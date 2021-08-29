# App Academy Open - Ruby Course

App Academy Open [Ruby Course](https://open.appacademy.io/learn/full-stack-online/ruby/setting-up-a-development-environment--phase-1-) notes.


## Glossary

**Stack** - Here at App Academy we work with a Ruby on Rails, JavaScript, React, Redux, and PostgresSQL stack. A [stack](https://en.wikipedia.org/wiki/Solution_stack) is simply a collection of software and hardware used in development of an application. For our specific purposes we are using Ruby on Rails on the backend/server, PostgresSQL to house our database, and JavaScript + React + Redux for frontend rendering and logic. For backend development in particular, we will need a database application, a server, and a web-application framework. For the purposes of this course, we will be using two database applications: PostgreSQL and SQLite.


## **Essential Terminology**

- **directory** - same as a folder; a directory can contain many files or subdirectories
- **root** - the outer most, main directory; opening a fresh terminal typically brings you into the root directory
- **path** - location on your computer specified by directories. `/Desktop/photos/cats.jpeg` is an example of a path

[Reference](https://open.appacademy.io/learn/full-stack-online/software-engineering-foundations/terminal-basics-notes)

___

## Tools

### Ruby
Yukihiro “Matz” Matsumoto released the first version of the Ruby programming language in 1995 in Japan. Ruby is dynamic, reflective, object-oriented, and multi-paradigm. [Non-technical overview](https://open.appacademy.io/learn/full-stack-online/ruby/nontechnical-overview-of-ruby).

### **Homebrew**
Homebrew is kind of like a low-tech App Store. It allows us access to and the ability to install a wide variety of software and command line tools from the console. These are distinct from those hosted on the App Store and will need to be managed by Homebrew.  Check out the [Homebrew website](https://brew.sh/) to learn the basic commands.

### **Git**
Git is a version control system that allows us to track, commit and revert changes to files within a directory.

### **VS Code**
This one is pretty easy. Go to [code.visualstudio.com](https://code.visualstudio.com/), then download and install VS Code.

To verify that the shell commands were installed correctly, run `which code` in your terminal. If `code` is not a recognized command, open the VS Code editor, open the Command Palette (`Cmd+Shift+P` on macOS ,`Ctrl+Shift+P` on Linux) and type `shell command` to find the `Shell Command: Install 'code' command in PATH` command. Then restart the terminal. This allows you to easily open files in VS Code from the terminal using the `code` command followed by a file or directory.

Next, we'll want to install a few useful VS Code extensions and configure VS Code to play nice with these extensions. Download [this zip file](https://assets.aaonline.io/fullstack/setup_vscode_master.zip), which contains a scripts that will do the work for you. Unzip the file and open the `setup_vscode` directory. Then open that directory in the terminal (drag and drop it over the terminal icon on macOS or right click in the directory and select `Open in Terminal` on most Linux distributions). To run the script, type `./setup_vscode.sh`. The script will do the rest. Simply restart VS Code and you'll be good to go. (Note that there's a second script, called `setup_vscode_linter.sh`. We can't run this script yet but will do so in due time.)

### **rbenv**
Here we will be setting up Ruby with the help of [rbenv](https://github.com/rbenv/rbenv), a Ruby environment manager. We like rbenv because it allows us to switch between versions of Ruby easily and setup default versions to use within project directories. This will install instances of Ruby in addition to the system version, which comes pre-installed.

### **PostgreSQL**
a fast, feature-rich, open-source database application. It is a scalable application that we can use for development and production apps. We will be using PostgreSQL for most of our web-apps.

Note: **For MacOS X**

Fortunately for MacOS X, we can use [Postgres.app](https://postgresapp.com/), which provides the database application and a command line interface (CLI) so we can interact with it. To install Postgres.app, download and follow the installation instructions from the website.

**Though the instructions say it is optional, it is highly recommended to configure your system `$PATH` so that you can use the command line tools.** We will make extensive use of them in the course.

Paste these commands into the terminal:

```
sudo mkdir -p /etc/paths.d &&
echo /Applications/Postgres.app/Contents/Versions/latest/bin | sudo tee /etc/paths.d/postgresapp
```

### **SQLite**

[SQLite](https://www.sqlite.org/about.html) is a small, lightweight database application that requires no configuration and stores the database as a stand-alone file. For this reason, we will be using SQLite for a few of our in-class projects.

Install using the Brew package manager:

```
brew install sqlite
```

Again, verify that installation was successful by opening the SQLite CLI.

```
# open SQLite CLI with this command
sqlite3

#  you should see this output
# SQLite version 3.16.0 2016-11-04 19:09:39
# Enter ".help" for usage hints.
# Connected to a transient in-memory database.
# Use ".open FILENAME" to reopen on a persistent database.

# .q to quit
sqlite> .q
```

### **Rails**

[Ruby on Rails](http://rubyonrails.org/) will serve as our application framework for this course. Rails is a very full-featured, opinionated framework that provides all the tools we need to create a complete web-app. These include an ORM (Object Relational Mapper - essentially we can continue to use Object Oriented Programming with respect to resources in our database), routing, a development server, and a templating engine.

Fortunately for us, Rails is available as a gem in the Ruby ecosystem. Let's install it, specifying the version so that we're all working in sync:

```
# install rails
gem install rails --version 5.2.3
rbenv rehash
# verify installation
which rails # => /Users/username/.rbenv/shims/rails
```

### **Node.js & NPM**

[Node.js](https://nodejs.org/en/) will be our local JavaScript engine. This is used to run JavaScript code and run associated node commands.

Again, we want to use a version manager with Node to help us manage potential conflicts between versions and dependencies. In this case we will be using [NVM](https://github.com/creationix/nvm) (Node Version Manager) to install/manage Node.js.

```
# download and run the official install script
curl -o- https://raw.githubusercontent.com/creationix/nvm/v0.33.6/install.sh | bash

# update your terminal config (you will now have access to the nvm command)
source ~/.bashrc

# install a stable version of node
nvm install 10.13.0

# set version 10.13.0 as default version
nvm use 10.13.0

# verify install/config
which node # => /Users/username/.nvm/versions/node/v10.13.0/bin/node
```

Node, like Ruby, comes with a package manager called [NPM](https://docs.npmjs.com/), which provides access to a whole ecosystem of libraries and tools we can use. NPM comes pre-bundled with Node, so there is no additional work for us to do. By default we don't need any additional packages installed and will be installing them on a per-project basis.

## **Gems**

There are a few gems we will want to access globally.

- **Bundler** allows us to define project dependencies inside a `Gemfile` and gives us a bunch of commands to update, remove and install them. Check out the [Bundler docs](http://bundler.io/docs.html) for more info.
- **Pry** is an alternative to the Irb (the default Ruby REPL). It is not only more powerful, but also easier to use than Irb and should be your go-to for running and debugging Ruby code. Check out the [Pry website](http://pryrepl.org/) for more info and a super useful tutorial.
- **Byebug** is feature-rich debugging tool for Ruby. With Byebug you can halt the execution of your code and inspect/track variables and the flow of execution. Lots of cool features in here, so check out the [Byebug docs](https://github.com/deivid-rodriguez/byebug)!

Let's install them.

```
gem install bundler pry byebug
```
- **Rails** - see Some Tools section in this doc.

____

## Key Highlights / Notes For You 💡

### [Option Hashes](https://open.appacademy.io/learn/full-stack-online/software-engineering-foundations/default-arguments-and-option-hashes-notes)

If you have a method that accepts a hash as an argument, you can **omit the braces when passing in the hash**:

```
def method(hash)
    p hash  # {"location"=>"SF", "color"=>"red", "size"=>100}
end

method({"location"=>"SF", "color"=>"red", "size"=>100})

# this also works:
method("location"=>"SF", "color"=>"red", "size"=>100)
```

This can really clean things up when you have other arguments before the hash:

```
def modify_string(str, options)
    str.upcase! if options["upper"]
    p str * options["repeats"]
end

# less readable
modify_string("bye", {"upper"=>true, "repeats"=>3}) # => "BYEBYEBYE"

# more readable
modify_string("bye", "upper"=>true, "repeats"=>3)   # => "BYEBYEBYE"
```

Combining this with the default arguments we covered in the previous section can make our code even more flexible:

```
def modify_string(str, options={"upper"=>false, "repeats"=>1})
    str.upcase! if options["upper"]
    p str * options["repeats"]
end

modify_string("bye")   # => "bye"
modify_string("bye", "upper"=>true, "repeats"=>3)   # => "BYEBYEBYE"
```
