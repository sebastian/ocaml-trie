# Hello
This is an implementation of a trie in OCaml.
It is a "reinvent the wheel" kind of project, as there already exists a [trie
implementation in OCaml](http://www.lri.fr/~filliatr/software.en.html), but it
served me very well as a learning project. If it can be useful for others, then
even better!

# Versioning
The implementation is still rather experimental, and comes with no guarantees.
Once it has stabilized a bit more, it will follow the [semantic versioning](http://semver.org/) guidelines. But that is for the future.

# How to use
The trie is implemented as a functor.
To use it you need to write a module with the following signature:

    module type TrieSig = sig
      type t 
      type b
      val to_list : t -> b list
      val from_list : b list -> t
    end

Explanation of the different values:

- `type t`: the type of the keys that are to be used
- `type b`: the key fragments, more on this later.
- `to_list`: a function that takes a key, and converts it into key fragments
  that can be used to store a value in a trie.
- `from_list`: a function that takes a list of key fragments, and reassembles
  them into a regular key, as originally provided by the user.

For an example of how to write a module like this, please have a look at the
`StringTrieFunctionality` module provided in the `trie.ml` source file.


## Trie functionality

Now, let us assume we are using the StringTrie module that is provided in the
trie source. I will show how to create an empty trie, add some data, and then
later query it.

    let trie = StringTrie.empty () in
    let updated_trie = StringTrie.add trie "key" ARBITRARY_VALUE in
    let value = StringTrie.get updated_trie "key" in
    assert (value = ARBITRARY_VALUE)

The trie also supports maps, and iterations through the values, and also has
a convenience method for creating a trie from a list of key-value pairs.

    let age_trie = StringTrie.from_list [("sebastian",26);("simone",22)] in
    StringTrie.get age_trie "sebastian"


# Good bye
I wish you luck using my trie implementation. If you get stuck, find mistakes
or have improvements to suggest, please don't hesitate to contact me.

Sebastian:

- Email: sebastian.probst.eide@gmail.com
- Twitter: @probst
