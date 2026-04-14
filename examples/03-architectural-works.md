# Example 3: When Did Architectural Works Become Copyrightable?

**Scenario**: A defendant argues that a building design was not copyrightable when the building was constructed in 1988. The repository settles the question.

## Step 1: Find every act that amended Section 102 (subject matter)

```
$ git log --oneline -- sections/102.md
b78c5fc Architectural Works Copyright Protection Act of 1990
6d717db Copyright Act of 1976
```

Only two commits have ever touched Section 102: the 1976 Act that created it, and the Architectural Works Copyright Protection Act that amended it.

## Step 2: See the diff from the Architectural Works Act

```
$ git diff b78c5fc~1 b78c5fc -- sections/102.md
```

```diff
 (5) pictorial, graphic, and sculptural works;
 (6) motion pictures and other audiovisual works;
-(7) sound recordings.
+(7) sound recordings; and
+(8) architectural works.
```

Before December 1, 1990, Section 102(a) listed exactly seven categories of copyrightable works. The Architectural Works Copyright Protection Act added the eighth: "architectural works."

## Step 3: Read the law as it existed during the disputed period

For a building constructed in 1988:

```
$ git show 6d717db:sections/102.md
```

This shows the version of Section 102 enacted by the 1976 Act, which remained unchanged through 1988. No category (8) exists.

## Conclusion

Architectural works were **not** a listed category of copyrightable subject matter until December 1, 1990. A building constructed in 1988 could not claim protection as an "architectural work" under Section 102 — though elements of it might have qualified as "pictorial, graphic, and sculptural works" under the pre-existing category (5), subject to the useful article doctrine.
