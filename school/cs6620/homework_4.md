# CodeQL

Install CodeQL CLI

Select and download zip file from [here](https://codeql.github.com/docs/codeql-cli/getting-started-with-the-codeql-cli/#getting-started-with-the-codeql-cli)

install unzip
```
> sudo apt-get install zip
```

unzip
```
> unzip codeql-linux64.zip
```


# Facebook Infer

* Spin up ubuntu docker instance
* install curl
* install xz-utils
* install dnsutils
* install tzdata
* run install commnad
```
VERSION=1.1.0; \
curl -sSL "https://github.com/facebook/infer/releases/download/v1.1.0/infer-linux64-v1.1.0.tar.xz" \
| tar -C /opt -xJ && ln -s "/opt/infer-linux64-v$VERSION/bin/infer" /usr/local/bin/infer
```
* install gcc
* install build-essential



### types of analysis
* Starvation (6) https://fbinfer.com/docs/next/checker-starvation/
* Linters (10) https://fbinfer.com/docs/next/checker-linters/
* Cost (10) https://fbinfer.com/docs/next/checker-cost/
* biabduction (10) https://fbinfer.com/docs/next/checker-biabduction
* bufferoverrun (19) https://fbinfer.com/docs/next/checker-bufferoverrun/
* self-in-block (5) https://fbinfer.com/docs/next/checker-self-in-block/
* annotation-reachability (4) https://fbinfer.com/docs/next/checker-annotation-reachability/
* printf-args (1) https://fbinfer.com/docs/next/checker-printf-args/
* config-checks-between-markers (1) https://fbinfer.com/docs/next/checker-config-checks-between-markers/
* config-impact-analysis (1) https://fbinfer.com/docs/next/checker-config-impact-analysis/
* pulse (10) https://fbinfer.com/docs/next/checker-pulse/
* quandry (22) https://fbinfer.com/docs/next/checker-pulse/
* liveness (1) https://fbinfer.com/docs/next/checker-liveness/
* dotnet-resource-leak (1) https://fbinfer.com/docs/next/checker-dotnet-resource-leak/
* eradicate (18) https://fbinfer.com/docs/next/checker-eradicate/
    * just for Java
    * type checker for @Nullable annotations
    * "the goal is to eradicate null pointer exceptions
* loop-hoisting (2) https://fbinfer.com/docs/next/checker-loop-hoisting/
* racerd (10) https://fbinfer.com/docs/next/checker-racerd/
* impurity (2) https://fbinfer.com/docs/next/checker-impurity/
* inefficient-keyset-iterator (1) https://fbinfer.com/docs/next/checker-inefficient-keyset-iterator/
* litho-required-props (1) https://fbinfer.com/docs/next/checker-litho-required-props/
* siof (1) https://fbinfer.com/docs/next/checker-siof/
* topl (1) https://fbinfer.com/docs/next/checker-topl/
* uninit (1) https://fbinfer.com/docs/next/checker-uninit/

* fragment-retains-view (1) https://fbinfer.com/docs/next/checker-fragment-retains-view/
    * android specific
* immutable-cast (1) https://fbinfer.com/docs/next/checker-immutable-cast/
    * for Java
* resource-leak-lab (1) https://fbinfer.com/docs/next/checker-resource-leak-lab/



### types of analysis to talk about 
* liveness
* uninit
    * liveliness and uninit seem to be related
* inefficient-keyset-iterator 
    * we might be able to talk about how specific we get with analysis
* quandry
    * taint analysis detects things like sql injection
* pulse
    * memory safety analysis
    * things like memory leaks
* racerd
    * finds data races


### Topl
Attempted example: https://fbinfer.com/docs/checker-topl

The taint.topl file looks like:
    
```
property Taint

prefix "Main"
start -> start: *
start -> tracking: source(Ret) => x := Ret
tracking -> error: sink(Arg, VoidRet) when x == Arg
```

The java code Main.java looks like
```
public class Main {
  static void f() { g(tito(source())); }
  static void g(Object x) { h(x); }
  static void h(Object x) { sink(x); }
  static Object tito(Object x) { return x; }
  static Object source() { return "dirty"; }
  static void sink(Object x) {}
}
```

we can run the analysis by this command
```
> infer --topl --topl-properties taint.topl  -- javac Main.java
> infer explore
```

One way to create a java program without errors is by doing:
```
public class Main {
  static void f() {
          Object x = source();
  }
  static void g() {
          sink(funk());
  }
  static Object source() { return "dirty"; }
  static Object funk() {return "of the funk"; }
  static void sink(Object x) {}
```