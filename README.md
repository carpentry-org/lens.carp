# lens

*Early WIP, also includes an implementation for Prisms on Maybes only*

A simple Lens library for Carp.

## Usage

```clojure
(load "git@github.com:hellerve/lens.carp@master")

(deftype Address [city String street (Pair String Int)])

(defn main []
  (let-do [addr (Lens.for Address street)
           stre (Lens.for Pair a)
           comp (Lens.compose &addr &stre)
           data (Address.init @"Berlin" (Street.init 10 @"Paul-Lincke-Ufer"))]
    (println* &(~(Lens.get &comp) &data))
    (println* &(~(Lens.set &comp) @&data @"no"))
    (println* &(Lens.over &comp @&data &(fn [a] (reverse &a))))
  )
)
```

<hr/>

Have fun!
