# DevOps toolchain

## Disclaimer

This is a list of various tools to use in DevOps-related activities I've used.
I try to create a list and write a brief review reflecting my opinion on these.

Note that it is not going to be comprehensive list nor is going to be neutral:
the list reflects my own opinion which may be different to anyone else's.
Comments are welcome but I don't think they are going to change my opinion on the matter.

## Configuration management

#### Puppet

http://puppetlabs.com/puppet/puppet-open-source

##### Pros
* Simple to understand by average sysadmin
* External node classifiers
* Hiera
* Puppetmaster holds the logs of all puppetruns done

##### Cons
* Very slow working
* Very hard to extend:
  * You can't redefine variables:
    * This forces you do define variables you never use to store temporary values
    * You have to use some weird stuff like inline ERB templates for simple actions like
      concatenating 2 strings
  * Custom function definitions not very powerful:
    * Values of `''`, `undef`, `false`, `nil` are implicitely converted to each other at function start and end
* Hard to debug if you are not careful enough constructing dependencies
* Hard to setup if you need something bigger than minimal setup
* Load is produced on puppetmaster and this means that it is not good at scaling
* Most of the community modules suck
* Development progress of the upstream is quite slow

##### Neutral features
* Dependency based evaluation
* Manual registration of nodes

##### Comments
* I have not used Puppet for more than a year so some of the problems can be fixed since that time.
* I see no sane reason to use Puppet except if you are already running large site using it.
  * If you need something simpler than Chef take Ansible or Salt instead.

#### Chef

http://www.getchef.com/

##### Pros
* Funded very well and evolves really quickly
* Very powerful
* Good community modules
* Easy to setup
* Easy to extend

##### Cons
* A bit scary to start if you've never worked with configuration management systems before
* Depends on tons of gems. This is no longer an issue starting from Omnibus-based Chef 11
* Chef server is quite large:
  * Runs something like 3-4 services
  * Besides that brings several large applications with itself: RabbitMQ, Solr, etc. Although you never need to configure these (see pros list)
* Stores production data in binary format
* You can't do much with it without using special bloated commandline tool (knife)
* Somewhat complicated evaluation during run

##### Neutral features
* Forces recommended workflow (run_list, environment, cookbooks, no flatfile actions)
* Have several flavours of clients (client+server, solo, zero, metal)
* Ruby used to write recipes

##### Comments
* I personally consider the Chef to be the tool you'd like to consider first of all when starting the new project

#### Ansible

http://www.ansible.com/home

TBD

### Other options

I have never used these so my opinions on these are based purely on impressions produced by docs and talks with other peole.

### Salt

http://www.saltstack.com/

* Looks good for Orchestration
* Seems to be the fastest of all tools

Not sure I'd like to try it as a configuration management tool but I'd definitely like
to try it as an orchestration tool.

### Pallet

http://palletops.com/

* Written in Clojure and runs atop JVM
* Development in the upstream looks to be a bit slow
* Several major companies use it

It looks very unusual and thus very interesting to try.
Clojure might make creating the configuration flows more natural than with the other tools.
At the same time it might be not so easy to use and extend.

### Misc tools

I don't consider and not going to use (unless I absolutely have to) very old tools (CFEngine, etc) or non-mainstream ones (Bcfg2) as well as small alternatives (babushka, sprinkle) so I don't describe them here.

## Alerting

## Metrics
