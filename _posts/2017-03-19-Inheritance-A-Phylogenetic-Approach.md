## Inheritance: A Phylogenetic Approach [^1]

[^1]: Originally written for Propelics and currently [posted](https://www.anexinet.com/blog/inheritance-a-phylogenetic-approach/) at Anexinet's Blog.

The rise of modern high-level object oriented programming languages (e.g., Java, C#, Swift) brought with it the enforcement of single-parent hierarchy and, from my point of view, that was the right path.

A class defines properties and attributes that individuals have in common, i.e., serves to **class**ify such individuals to belong to certain kind. In terms of software architecture, one could make the argument—against single-parent inheritance—that a complex object might have the need to be able to fit the classification of two kinds and thus, perform tasks from both classes. For the sake of argument, let’s set aside for a moment the possibly unmaintainable implications of such approach and focus on the exact argument because, in a single-parent hierarchy, it is still possible for an object to fit the classification of two or more kinds: their direct parent and their parent’s, and their parent’s, and so forth. It is a matter of a good ground-up hierarchy design to be able to discern which methods are required to have a base implementation (from an abstract class), and which ones only require to have its capabilities as a group publicly known (from their interface definition).

I like to take the example of a phylogenetic tree to explain to my audience what a good hierarchical framework looks like. Our starting point would be last universal ancestor of the tree of life.

```csharp
    /// <summary>
    /// The last universal ancestor of all living organisms.
    /// </summary>
    abstract class LastUniversalAncestor
    {
    }
```

Moving from there, we found three life domains: Archaea, Bacteria, and Eukarya. These domains have descriptions which strictly classify members in such a way that, the member of one domain cannot belong to any of the other two. 

```csharp
    /// <summary>
    /// Describes the members of the Eukarya Domain.
    /// </summary>
    abstract class Eukarya : LastUniversalAncestor
    {
        // Uniquely identifying set of characteristics of Eukarya organisms
        // E.g., consist of eukaryotic cells.
    }

    /// <summary>
    /// Describes the members of the Archaea Domain.
    /// </summary>
    abstract class Archaea : LastUniversalAncestor
    {
        // Uniquely identifying set of characteristics of Eukarya organisms
        // E.g., consist of prokaryotic cells.
    }

```

As we traverse the tree, we found this strict description/classification happening at all the ranks throughout the hierarchy (Kingdom, Phylum, Class, Order, Family, Genus, Species) and so should each of our framework’s subtrees. It is up to the architect to capture which properties best differentiates one subtree from the others. For instance, the Eukarya domain consist of organism consisting of eukaryotic cells. 

```csharp
    /// <summary>
    /// Describes the members of the Animalia Kingdom.
    /// </summary>
    abstract class Animalia : Eukarya
    {
        // Uniquely identifying set of characteristics of animals
        // E.g., ingest other organisms or their products to survive.
    }

    /// <summary>
    /// Describes the members of the Chordata Phylum.
    /// </summary>
    abstract class Chordata : Animalia
    {
        // Uniquely identifying set of characteristics of chordates
        // E.g., possess a hollow dorsal nerve cord.
    }

    /// <summary>
    /// Describes the members of the Mammalia Class.
    /// </summary>
    abstract class Mammalia : Chordata
    {
        // Uniquely identifying set of characteristics of mammals
        // E.g., possess mammary glands.
    }
```

Perhaps, the reader will notice that all these classes are `abstract`, that is, they cannot be directly instantiated and there is a good reasoning behind this: there is no such thing as pure animal; an animal must belong to its respective phyla, class, et al. Let’s jump to the species level and take a closer look at a random one: *Leptonycteris nivalis*. If we were to have one pet of this species of bat, we would most likely name it. In the same manner, an instance of a class is named and, from here, it can be inferred that, a species kind of class must be able to be instantiated.        

```csharp
    // ...
    LeptonycterisNivalis Buddy = new LeptonycterisNivalis();
    // ...
```

But now, bats fly and so do birds but as we all know, bats are not birds. Is our classification system flawed? Well, no. We just need to find out the common ancestor within a given subtree to all species that fly and specify that as a capability. In this case, all members of the Order Chiroptera fly.

```csharp
    interface Flies
    {
        void Fly();
    }

    abstract class Phyllostomidae : Chiroptera, Flies
    {
        public abstract void Fly();
    }

    abstract class Leptonycteris : Phyllostomidae
    {
        // ...
    }

    /// <summary>
    /// Describes a Mexican long-nosed bat.
    /// </summary>
    class LeptonycterisNivalis : Leptonycteris
    {
        public override void Fly()
        {
            // ...
        }
    }
```

That same `Flies` interface may be re-used in all hierarchical sub-trees which contain a flying species and, in the same manner, provide a common implementation—if applicable—for all subtrees that would perform the action in a similar way.
