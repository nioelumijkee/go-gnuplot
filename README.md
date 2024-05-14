go-gnuplot
==========

Simple-minded functions to work with ``gnuplot``.
``go-gnuplot`` runs ``gnuplot`` as a subprocess and pushes commands
via the ``STDIN`` of that subprocess.

See http://www.gnuplot.info for more informations on the
exact semantics of these commands.

Example
--------

```go
package main

import "github.com/sbinet/go-gnuplot"
import "fmt"

func main() {
	fname := ""
	persist := false
	debug := true

	p,err := gnuplot.NewPlotter(fname, persist, debug)
	if err != nil {
		err_string := fmt.Sprintf("** err: %v\n", err)
		panic(err_string)
	}
	defer p.Close()

	p.PlotX([]float64{0,1,2,3,4,5,6,7,8,9,10}, "some data")
	p.CheckedCmd("set terminal pdf")
	p.CheckedCmd("set output 'plot002.pdf'")
	p.CheckedCmd("replot")


	p.CheckedCmd("q")
	return
}
```

![plot-t-002](https://github.com/nioelumijkee/go-gnuplot/raw/master/examples/imgs/plot002.png)


Documentation
-------------

API documentation can be found here:

 http://godoc.org/github.com/sbinet/go-gnuplot

