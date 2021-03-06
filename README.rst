========
R-trader
========

About
-----
Mechanical Trading System using R (prototype for fun and learning purposes)

Dependencies
------------
- R (quantmod, RSQLite)
- SQLite3
- Node.js (sqlite3, node-static)
- jqPlot
- JQuery UI

R Setup
-------
From inside **R-trader/data** directory, create sample data base typing::

 [irocha@napoleon data (master)]$ ./createsqlitedb.sh 
 Cleaning up...
 Extracting SQL file...
 Generating csv from SQL file...
 Creating SQLite3 database...
 Removing temporary files...
 Done.

**IMPORTANT**: real *(swing)* data from **BOVESPA** since 1994-01-03 (until 2011-06-17)

After installing R packages (command: **install.packages(c("RSQLite", "quantmod"))**), from inside **R-trader** base directory type::

 [irocha@napoleon R-trader (master)]$ R

 R version 2.12.1 (2010-12-16)
 Copyright (C) 2010 The R Foundation for Statistical Computing
 ISBN 3-900051-07-0
 Platform: i686-pc-linux-gnu (32-bit)

 R is free software and comes with ABSOLUTELY NO WARRANTY.
 You are welcome to redistribute it under certain conditions.
 Type 'license()' or 'licence()' for distribution details.

   Natural language support but running in an English locale

 R is a collaborative project with many contributors.
 Type 'contributors()' for more information and
 'citation()' on how to cite R or R packages in publications.

 Type 'demo()' for some demos, 'help()' for on-line help, or
 'help.start()' for an HTML browser interface to help.
 Type 'q()' to quit R.

 Loading required package: quantmod
 Loading required package: Defaults
 Loading required package: xts
 Loading required package: zoo
 Loading required package: stats

 Attaching package: 'zoo' 

 The following object(s) are masked from 'package:base':

     as.Date

 Loading required package: TTR
 Loading required package: RSQLite
 Loading required package: DBI

To view all technical analisys charts, type inside **R**::

 > test()

**IMPORTANT**: remember to change your project directory inside files::

 [irocha@napoleon R-trader (master)]$ more .Rprofile 
 options(papersize="a4")
 options(editor="emacs")
 options(pdfviewer="evince")

 .First <- function() {
   require(quantmod)
   require(RSQLite)
   setwd("/home/irocha/git/R-trader")  <<< change this!
   source("trader.r")
 }
 
 [irocha@napoleon R-trader (master)]$ more trader.r 
 t <- function() {
   source("trader.r")
 }

 STK <- "PETR4"

 # remember to change dbname! <<< SQLite sample database complete path
 gs <- function(symbol, dbname="./data/symbols.db", limit=0, begin="", end="") { 
   conn <- dbConnect("SQLite", dbname)
   ...


Node Setup
----------

After installing `node.js <http://nodejs.org/>`_, install node.js package manager **npm** typing::

 [irocha@napoleon ~]$ curl http://npmjs.org/install.sh | sh
  % Total    % Received % Xferd  Average Speed   Time    Time     Time  Current
                                 Dload  Upload   Total   Spent    Left  Speed
 100  3927  100  3927    0     0   4773      0 --:--:-- --:--:-- --:--:-- 11252
 fetching: http://registry.npmjs.org/npm/-/npm-1.0.27.tgz
 0.4.11
 1.0.27
 cleanup prefix=/data/node

 This script will find and eliminate any shims, symbolic
 links, and other cruft that was installed by npm 0.x.

 Is this OK? enter 'yes' or 'no' 
 yes

 All clean!
 ! [ -d .git ] || git submodule update --init --recursive
 node cli.js rm npm -g -f
 node cli.js cache clean
 node cli.js install -g -f
 /data/node/bin/npm_g -> /data/node/lib/node_modules/npm/bin/npm.js
 /data/node/bin/npm-g -> /data/node/lib/node_modules/npm/bin/npm.js
 /data/node/bin/npm -> /data/node/lib/node_modules/npm/bin/npm.js
 npm@1.0.27 /data/node/lib/node_modules/npm 
 It worked

Install **node.js** dependencies typing::

 [irocha@napoleon ~]$ npm install sqlite3 node-static

 > sqlite3@2.0.16 preinstall /home/irocha/node_modules/sqlite3
 > node-waf clean || true; node-waf configure build

 Nothing to clean (project not configured)
 Setting srcdir to                        : /home/irocha/node_modules/sqlite3 
 Setting blddir to                        : /home/irocha/node_modules/sqlite3/build 
 Checking for program g++ or c++          : /usr/bin/g++ 
 Checking for program cpp                 : /usr/bin/cpp 
 Checking for program ar                  : /usr/bin/ar 
 Checking for program ranlib              : /usr/bin/ranlib 
 Checking for g++                         : ok  
 Checking for node path                   : not found 
 Checking for node prefix                 : ok /data/node 
 Checking for sqlite3                     : yes 
 'configure' finished successfully (0.056s)
 Waf: Entering directory `/home/irocha/node_modules/sqlite3/build'
 [1/4] cxx: src/sqlite3.cc -> build/default/src/sqlite3_1.o
 [2/4] cxx: src/database.cc -> build/default/src/database_1.o                                                            
 [3/4] cxx: src/statement.cc -> build/default/src/statement_1.o                                                          
 [4/4] cxx_link: build/default/src/sqlite3_1.o build/default/src/database_1.o build/default/src/statement_1.o -> build/default/sqlite3_bindings.node                                                                                             
 Waf: Leaving directory `/home/irocha/node_modules/sqlite3/build'                                                        
 'build' finished successfully (1.678s)
 node-static@0.5.9 ./node_modules/node-static 
 sqlite3@2.0.16 ./node_modules/sqlite3 

To plot Candlestick chart, from inside **R-trader/js** directory, type::

 [irocha@napoleon js (master)]$ node server.js 
 jstrader listening on 8080...

Point your browser to `http://localhost:8080/stats.html <http://localhost:8080>`_, click **Show...** and have fun...

Author
------
Ivan Ribeiro Rocha <ivan.ribeiro@gmail.com> 

Copyright and License
---------------------

Copyright 2012 Ivan Ribeiro Rocha

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

   http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
