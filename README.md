# Otariinae
> Deploy Server
## Project Details
```
┌──────────────────────────────────────────────────────────────────────┐
│┼────────────────────────────────────────────────────────────────────┼│
││######:   ##    ##    :##:     :####:   ########             .###   ││
││#######:  ##    ##     ##     :######   ########             ####   ││
││##   :##  ##    ##    ####    ##:  :#   ##                   #:##   ││
││##    ##  ##    ##    ####    ##        ##                     ##   ││
││##   :##  ##    ##   :#  #:   ###:      ##                     ##   ││
││#######:  ########    #::#    :#####:   #######                ##   ││
││######:   ########   ##  ##    .#####:  #######                ##   ││
││##        ##    ##   ######       :###  ##                     ##   ││
││##        ##    ##  .######.        ##  ##                     ##   ││
││##        ##    ##  :##  ##:  #:.  :##  ##                     ##   ││
││##        ##    ##  ###  ###  #######:  ########            ########││
││##        ##    ##  ##:  :##  .#####:   ########            ########││
│┼────────────────────────────────────────────────────────────────────┼│
└──────────────────────────────────────────────────────────────────────┘

┌───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┐
│┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼│
││                                                                                                                                                     ││
││                                ┌──────────────────────┐          ┌─────────────────────────┐            ┌──────────────────────────────┐            ││
││                      ┌─────────┤                      │          │   pool receive request  │            │  web hook call api when      │            ││
││                      │         │   deploy controller  │◄─────────┤   from other platform   │◄───────────┤     PR create or push master │            ││
││                      │         │                      │          │                         │            └──────────────────────────────┘            ││
││                      │         └──────────────────────┘          └─────────────────────────┘                                                        ││
││                      │                      ▲                        ▲                                                                              ││
││                ┌─────┴─────────┐            │                        │      ┌────────────┬────────────────────────────────────────────────────────┐ ││
││                │               │            │                        │      │ API SERVER │                                                        │ ││
││        ┌───────┤ system call   ├─────────┐  └────────────┐           │      ├────────────┘                                                        │ ││
││        │       │               │         │               │           │      │  * POST: route ["/:organization/:repo/"]                            │ ││
││        │       └────────┬──────┘         ▼               │           │      │          + attach `GITHUB CONTEXT`                                  │ ││
││        │                │        ┌────────────┐          │           │      │                                                                     │ ││
││        ▼                ▼        │            │          │           └──────┤  * GET:  route ["/:organization/:repo/deployments/"]                │ ││
││  ┌────────────┐   ┌────────────┐ │   repo 3   │          │                  │                                                                     │ ││
││  │            │   │            │ │            │ ┌────────┴─────────┬─────┐  │                                                                     │ ││
││  │   repo 1   │   │   repo 2   │ └────────────┘ │ DEPLOY CONTROLLER│     │  │  * GET:  route ["/:organization/:repo/deployments/:hash_commit"]    │ ││
││  │            │   │            │                ├──────────────────┘     │  │                                                                     │ ││
││  └────────────┘   └────────────┘                │ * check repo           │  │                                                                     │ ││
││                                                 │     + not exist: clone │  │  * GET:  route ["/:organization/:repo/deployments/:hash_commit/log"]│ ││
││                                                 │     + exist: pull      │  │                                                                     │ ││
││                                                 │ * deploy scrip         │  └─────────────────────────────────────────────────────────────────────┘ ││
││                                                 │ * deploy env           │                                                                          ││
││                                                 └────────────────────────┘                                                                          ││
││                                                                                                                                                     ││
│┼─────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┼│
└───────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────────┘
```
