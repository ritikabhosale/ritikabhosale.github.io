---
title: "Abstract Factory"
date: 2024-10-20T13:01:48+05:30
draft: false
---

Imagine you have different types of related products, and each product comes in different variants. If you want to ensure that you use products of the same variant throughout your program, the `Abstract Factory` design pattern can help.

In this pattern, there are different factories that produce different variants of these products. For example, consider Puma and Nike as factories. The Puma factory will manufacture Puma shoes and Puma shirts, while the Nike factory will manufacture Nike shoes and Nike shirts.

The key idea is that the base factory is responsible for producing both shoes and shirts, regardless of whether it's Puma or Nike. The client code doesn't need to know which specific factory is being used. To achieve this, we create a Factory interface that defines the behavior common to all factories. 

```go
type BBrandFactory interface {
	makeShoe() BShoes
	makeShirt() BShirt
}
```

Then, we implement this interface in concrete factory classes (e.g., PumaFactory, NikeFactory), each responsible for producing its specific product variants.

```go
type PumaFactory struct{}

func (pf PumaFactory) makeShoe() BShoes {
	return PumaShoes{}
}

func (pf PumaFactory) makeShirt() BShirt {
	return PumaShirt{}
}
```

For each product type (like shoes or shirts), we also create a base product interface (e.g., Shoes), which defines the common behavior for all shoes.

```go
type BShoes interface {
	setLogo()
	setMaterial()
}
```

Then, we create concrete product classes (e.g., NikeShoes, PumaShoes) that implement this interface, representing the specific variants produced by each factory.

```go
type PumaShoes struct{}

func (ps PumaShoes) setLogo() {
	println("setLogo for puma shoes")
}

func (ps PumaShoes) setMaterial() {
	println("setMaterial for puma shoes")
}
```

The concrete factories implement the process of manufacturing shoes and shirts in a way that is specific to each factory. They return concrete products like NikeShoes or PumaShoes without the client code needing to know which factory is in use. The client only interacts with the products via the base interface (Shoes), allowing the factory details to remain abstract.

Once all the factories and products are set up, you can easily switch between different factories to manufacture consistent product variants across your entire application. This switch can happen at the start of your app based on configuration settings, or dynamically, depending on your use case.

```go
func GetBrandFactory(brand string) (BBrandFactory, error) {
	switch brand {
	case "puma":
		return PumaFactory{}, nil
	case "nike":
		return NikeFactory{}, nil
	}

	return nil, errors.New("invalid brand value")
}

func main() {
	factory, _ := GetBrandFactory("puma")

	shoes := factory.makeShoe()
	shoes.setLogo()
	shoes.setMaterial()
}

```