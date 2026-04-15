# Example 7: When Did DMCA Safe Harbors Appear?

**Scenario**: A platform operator is sued for user-uploaded infringing content hosted in 1997. They claim protection under Section 512's safe harbor provisions. The plaintiff argues those protections didn't exist yet. Who's right?

## Step 1: Check whether Section 512 existed

```
$ git log --oneline -- sections/512.md
79fc3f2 Copyright Cleanup, Clarification, and Corrections Act of 2010
fb66fcc Technical Corrections to Title 17 Act of 1999
975fefd (tag: v1998-dmca) Digital Millennium Copyright Act of 1998 (DMCA)
```

Section 512 was created entirely by the DMCA in 1998 — it did not exist before.

## Step 2: Verify the section didn't exist before the DMCA

```
$ git show 975fefd~1:sections/512.md
```

This fails with an error — confirming that there was no Section 512 before the DMCA commit. The safe harbor framework did not exist in 1997.

## Step 3: Read the safe harbor as created

```
$ git show 975fefd:sections/512.md
```

Section 512 established four safe harbors for online service providers:

- **(a) Transitory Digital Network Communications** — mere conduit (routing, transmitting)
- **(b) System Caching** — intermediate and temporary storage
- **(c) Information Residing on Systems or Networks At Direction of Users** — hosting user-uploaded content
- **(d) Information Location Tools** — linking to infringing material

## Step 4: Check whether Section 512 has been amended since

```
$ git log --oneline -- sections/512.md
79fc3f2 Copyright Cleanup, Clarification, and Corrections Act of 2010
fb66fcc Technical Corrections to Title 17 Act of 1999
975fefd (tag: v1998-dmca) Digital Millennium Copyright Act of 1998 (DMCA)
```

Only two minor corrections afterward.

## Conclusion

The platform operating in 1997 cannot claim Section 512 protection — it did not exist yet. The DMCA was signed into law on October 28, 1998. Before that date, there was no statutory safe harbor for service providers, and platform liability was governed by common law and a handful of circuit court decisions.

The commit boundary makes the answer unambiguous: before commit `975fefd`, the file `sections/512.md` does not exist.
