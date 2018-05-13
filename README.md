# lando [![Build Status](https://travis-ci.org/softprops/lando.svg?branch=master)](https://travis-ci.org/softprops/lando) [![Coverage Status](https://coveralls.io/repos/github/softprops/lando/badge.svg)](https://coveralls.io/github/softprops/lando) [![crates.io](https://img.shields.io/crates/v/lando.svg)](https://crates.io/crates/lando) [![docs.rs](https://docs.rs/lando/badge.svg)](https://docs.rs/lando)

> aws lambda gateway api trigger interfaces for [Rustlang](https://www.rust-lang.org) applications

## [Documentation](https://softprops.github.io/lando)


> this project is currently under construction 🚧 👷🏿‍♀️ 👷🏽 👷‍♀️ 👷 🚧

## 🤔 about

Lando is a crate for HTTP server application.

A number of really great HTTP server crates exist in the [Rust ecosystem](https://crates.io/categories/web-programming::http-server).
You should check them out!
A property they all share is providing both interfaces for authoring applications,
as well a configuring a server to run your application.
A server which is then your reponsiblity to figure out how to host, scale,
monitor and manage operations and uptime for.

Lando is different. Lando's focus is purely on your application.

Servers, host management, and operations are all things which fall under the
the umbrella of
[undifferentiated heavy lifting](https://www.cio.co.nz/article/466635/amazon_cto_stop_spending_money_undifferentiated_heavy_lifting_/).
In other words, these are all things that do no really set you apart. Fortuntely,
there are services like AWS lambda which manage these for you so that you can instead
focus on what does differeniate you, your application.

Lando is designed to work within strong existing ecosystems, both with Rust as well as
the strong serverless ecosystems that extend beyond Rust ( make some friends! ).

Lando's interfaces are based the [http](https://crates.io/crates/http) crate
which is designed as a framework agnostistic and extensible http library and extends
the existing work of the [crowbar](https://crates.io/crates/crowbar) crate which
provides needed machinery to easily embed a rust application with one of lamdbas
[lowest overhead runtimes](https://theburningmonk.com/2017/06/aws-lambda-compare-coldstart-time-with-different-languages-memory-and-code-sizes/),
python 3.6.

A large and mature ecosystem of tooling already exists that works well with AWS lambda,
including flowflow tools like [the serverless toolkit](https://serverless.com/).
Lando does not intend to replace these but instead to work well with them 👫🏾.

You may ask what makes Rust a suitable choice for Lambda?
The AWS cost model for lambda is based on two factors: size and speed.
Lambda has a pay per usage cost model billing based on function size and execution time.
As a systems language, Rust is well designed specifically for these needs. As a highly embeddable
language, its interop story for runtimes like python's is 💖.

What this means for developers and organizations you is cost savings for engineers in
in terms of time spent focusing on applications an cost savings for organizations
on effcient spending.


## 📦  install

Add the following to your `Cargo.toml` file.

```toml
[lib]
name = "lambda"
crate-type = ["cdylib"]

[dependencies]
lando = "0.1"
cpython = "0.1"
```

> 💡 You may be new to the `cdylib` crate type. This allows rust compile and [link](https://doc.rust-lang.org/reference/linkage.html) your application as a shared object file `*.so` allows it to be included in the AWS python 3.6 [lambda runtime](https://docs.aws.amazon.com/lambda/latest/dg/current-supported-versions.html)

## 👩‍🔬 create

Lando defines a single macro named `gateway!` which exports a Rust function or
closure to a cpython initializer for use within an aws lambda.

```rust
#[macro_use(gateway)] extern crate lando;
#[macro_use] extern crate cpython;

gateway!(|request, _context| {
  println!("{:?}", request);
  Ok(lando::Response::new(()))
);
```

## 🚀 deploy

## Roadmap

```
[x] expose typesafe interface for API gateway handlers
[ ] expose API gateway interface adapting to Rust's http crate
```

Doug Tangren (softprops) 2018
