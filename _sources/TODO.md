# TODO

- IMPORTANT
  - ICharCipher should be char -> char not char -> string. This makes it MUCH easier to make good points in regards to dependency injection and in terms of generics.
  - (!!!!) Replace all 404 images with placeholder images as in chapter on generics e.g.
- CONTEMPLATE
  - Harmonize subchapter of chapters:
    0. Executive summary
    1. Motivation (problem)
    2. Definition
    3. Examples
    4. Exercises
- General
  - Add a license. Ex: https://creativecommons.org/licenses/by-nc-nd/4.0/
  - Links to official documentation like in the [Type Systems](type-systems) chapter?
  - Add "decode" method to all usages of Caesar cipher. This is important because it helps students think about reusability.
  - Static interface methods? https://docs.microsoft.com/en-us/dotnet/csharp/whats-new/tutorials/static-virtual-interface-members
  - Separation of concerns. First mentioned in static methods chapter.
- Interfaces
  - "Default interface methods"
    - https://learn.microsoft.com/en-us/dotnet/csharp/language-reference/proposals/csharp-8.0/default-interface-methods
    - https://en.wikipedia.org/wiki/Trait_(computer_programming)
    - https://scg.unibe.ch/archive/papers/Scha03aTraits.pdf
- Subtype polymorphism
  - **More about replace conditional with polymorphism?**
  - Extract intro part on polymorphism from Subtype polymorphism chapter into its own chapter?
  - Refer to Types and Programming Languages by Benjamin Pierce, chapter 22 on polymorphism. Defines substitution.
- Data types
  - Should discuss Reflection?
  - Expand discussion in Data Types chapter on why treating Nullable warnings as errors is a good idea and that this should be the default.
  - Have I emphasized the importance of null reference static analysis enough?
- Compilation
  - Compiler warnings in Compilation chapter.
  - P. 49, section 4.3 of Types and Programming Languages. Bejamin Pierce. Image on how we go from characters on a file to a program that's being printed on screen.
- Indirect object composition
  - Relate to Inversion of Control (IoC).
- Object composition
  - Clarify that we are not talking about merely instantiating another object in an instance method but rather storing an object as an instance variable (meaning as a property or in a field).
  - Perhaps discussion on Dependency should be its own chapter? How does this relate to how we use the term dependency in the context of coupling?
  - "Constructed" could mean that you call someone who constructs. If the thing you call to construct is constructed in you then it's still a "hard" dependency.
  - Use term "collaborator".
- General
  - Reintroduce error code in prefix of printed errors.
  - There is no information on what "keyword" means.
- Sets
  - Perhaps "business objects" is a poor choice of words.
- Variables
  - Variables chapter missing image placeholders.
- Type-checking
  - On the purpose of types: http://www.cse.chalmers.se/edu/year/2011/course/TIN321/lectures/proglang-07.html
  - More about Type Safety. How even addings strings and ints is type safe in some languages. It all depends.
    - Admit that there are multiple definitions. In e.g. the documentation on [Generics] (https://learn.microsoft.com/en-us/dotnet/standard/generics/) they say that generics increase type safety when comparing to non-generic collections like ArrayList. Here they are using the definition that would consider dynamic languages non-type safe. But there is also the definition that leads to treating dynamic langauges (or even almost all) as being type safe. The latter is more about memory safety. Type safety I guess should be its own chapter.
    - Referera till Types and Programming Languages, Benjamin Pierce. 8.3. sid 95. Safety = Progress + Preservation.
    - Makes more sense if we divide it into compile-time type safety and run-time type safety. This makes the concept of unsafe much more sensible. It also makes the concept of uni-typed much more sensible since we can talk about compile-time uni-typed and run-time uni-typed. Not sure what compile-time poly-typed + run-time uni-typed would mean though.
    - https://en.wikipedia.org/wiki/Type_system#Type_safety_and_memory_safety
    - https://web.archive.org/web/20211218122334/http://www.pl-enthusiast.net/2014/08/05/type-safety/
    - https://web.archive.org/web/20211124135419/http://www.pl-enthusiast.net/2014/07/21/memory-safety/
    - https://en.wikipedia.org/wiki/Type_safety
    - https://stackoverflow.com/questions/260626/what-is-type-safe
    - https://courses.cs.washington.edu/courses/cse341/04wi/lectures/26-unsafe-languages.html
    % Det korta svaret ang type safe är att ett språk som är type safe garanterar att alla program skrivna i språket är semantiskt väldefinierade. Om man t.ex. deklarerar en variabel utan att tilldela den ett värde och sen försöker använda den i C# (statiskt typat) så får man ett kompileringsfel. Om man gör samma sak i t.ex. Python eller Ruby (dynamiskt typat) så får man ett exception. Oavsett om det är ett run-time eller ett compile-time fel så är det ett språk som definierats av språket i förhand. Om det inte finns en definition i språket så är det programmet inte väldefinierat och detta
    - https://nddoornekamp.medium.com/typing-static-or-dynamic-strong-or-weak-safe-or-unsafe-f2fbca7182f6
- Type systems
  - Strong vs weak
- Labs
  - Brute-force hangman. Computer does guessing. You input how long the word should be and the program already has a word list stored.
  - Smart hangman. Like simple hangman but guessing computer uses word list and probability theory to make the best guesses.

```csharp
class CaesarCipher : ICipher<char,char>
{
  int steps;
  string alphabet = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";
  public CaesarCipher (int steps) => this.steps = steps;
  public char Encode (char input)
  {
    int index = alphabet.IndexOf(Char.ToUpper(input));
    if (index == -1) return input;
    int newIndex = (index + steps) % alphabet.Length;
    if (Char.IsUpper(input))
      return alphabet[newIndex];
    else
      return Char.ToLower(alphabet[newIndex]);
  }
}
```