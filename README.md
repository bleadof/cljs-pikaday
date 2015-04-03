# cljs-pikaday

cljs-pikaday is intended to provide a native ClojureScript interface to the 
[Pikaday](https://github.com/dbushell/Pikaday) JavaScript date picker, intended 
for use in the various ClojureScript react frameworks.

The implementation currently works for 
[reagent](https://github.com/reagent-project/reagent) (I'm hoping to add an 
[Om]() implementation soon, and maybe a nicer interface for 
[re-frame](https://github.com/Day8/re-frame)).

## reagent interface

The reagent implementation accepts an ratom 
(or [reaction](https://github.com/Day8/re-frame#how-flow-happens-in-reagent))
as its input, and `reset!`s it whenever the selected date changes.

The simplest way to use it would be something like this:

```clojure
(ns cljs-pikaday.core
    (:require [reagent.core :as reagent]
              [cljs-pikaday.reagent :as pikaday]))

(defonce the-date (reagent/atom (js/Date.)))

(defn home-page []
  [:div [:h2 "Select a date"]
    [pikaday/date-selector {:date-atom the-date}]])

(reagent/render [home-page] (.getElementById js/document "app")))
```

`pikaday/date-selector` returns hiccup for an `<input>` tag, and 
sets up various reagent lifecycle methods to instantiate and bind 
a `Piakaday` instance. When the user selects a new date in the input 
field, the atom passed in to the `:date-atom` property will be 
`reset!` with its new value.

`cljs-pikaday` currently uses plain JavaScript `Date` objects for 
its values - I'd like to have it able to use cljs-time and/or 
moment at some point.

## TODO

* document min/max date atoms
* Move example project to its own directory
* Push to clojars
* Om interface
