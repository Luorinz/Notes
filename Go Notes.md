1. given a map from string to bool, how to iterate over it and print out all the key-values? 

```Go 
package main

import "fmt"

func main() {
	m := make(map[string]bool)
	m["jack"] = true
	m["john"] = false
	
	for k, v := range m {
		fmt.Println(k, v)
	}
}
```

2. given an array (slice) how to iterate all of its values?

```Go
package main

import "fmt"

func main() {
	l := []string{"a", "b", "c"}
	
	for _, v := range l {
		fmt.Println(v)
	}
}
```

3. How to reduce the line of codes for this program

```Go
conn, err := os.Open("/tmp/file")
if err != nil {
      panic(err)
} else {
      conn.Read()
}
array := []string{}
x := array[0]
y := array[1]
z := array[2]
fmt.Printf("%s %s %s\n", x, y, z)


if conn, err := os.Open("/tmp/file"); err != nil {
      panic(err)
}
conn.Read()
array := []string{}
x, y, z := array[0], array[1], array[2]
fmt.Printf("%s %s %s\n", x, y, z)
```

4. how to append a value to a slice (array)

```Go
array := []int{}
append(array, 1)

```