# build-uber-log4j2-handler

A conflict handler for log4j2 plugins cache files for the `uber` task of `tools.build`.

Log4j2-based libraries often have a `Log4j2Plugins.dat` file, containing a cache of
formatting plugins. If you build an uberjar containing more then one of these files,
you need this conflict handler in order to merge those files correctly.

> Note: requires a version of `tools.build` that supports `:conflict-handlers`!

## usage

Add the following dependency to your `:build` alias:

```clojure
  io.github.seancorfield/build-uber-log4j2-handler {:git/tag "v0.1.0" :git/sha "..."}
```

In your `build.clj` script, require the handler:

```clojure
(ns build
  (:require [clojure.tools.build.api :as b]
            [org.corfield.log4j2-conflict-handler
              :refer [log4j2-conflict-handler]])
```

and then pass it to the `tools.build` `uber` task:

```clojure
  (b/uber {... :conflict-handlers log4j2-conflict-handler ...})
```

## license

Copyright © 2021 Sean Corfield

Distributed under the Apache Software License version 2.0.
