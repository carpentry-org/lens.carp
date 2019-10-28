# lens

*Early WIP, also includes an implementation for Prisms on Maybes only*

A simple Lens library for Carp.

## Usage

```clojure
(load "git@github.com:hellerve/lens.carp@master")

(deftype Address [
  city String
  street (Pair String Int)]
)

(defn main []
  (let-do [addr (Lens.for Address street)
           stre (Lens.for Pair a)
           comp (Lens.compose &addr &stre)
           data (Address.init @"Berlin" (Pair.init @"Paul-Lincke-Ufer" 10))]
    (IO.println &(str (Lens.get &comp &data)))
    (IO.println &(str &(Lens.set &comp &data @"Maybachufer")))
    (IO.println &(str &(Lens.update &comp &data &reverse)))
  )
)
```

<hr/>

Have fun!
