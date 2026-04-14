# Example 2: Tracing the History of a Single Provision

**Scenario**: You need to know when and how §302 (copyright duration for works created on or after January 1, 1978) has been amended. Identifying the acts that touched a provision is a common first step in legislative history research before pulling committee reports, floor debate, and secondary sources.

## Step 1: List every act related to §302

```
$ git log --oneline -- sections/302.md
8a620fb Sonny Bono Copyright Term Extension Act of 1998
6d717db Copyright Act of 1976
```

There are two commits total, so §302 has been amended exactly once since 1976.

## Step 2: See the original 1976 text

```
$ git show v1976:sections/302.md
```

## Step 3: See exactly what the CTEA changed

```
$ git diff --word-diff v1998-ctea~1 v1998-ctea -- sections/302.md
```

Word-diff highlights the substitutions inline. The Sonny Bono Copyright Term Extension Act of 1998 made changes like these:

```
(a) In General.-...endures for a term consisting of the life of the
author and [-fifty-]{+70+} years after the author's death.

(b) Joint Works.-...the copyright endures for a term consisting of
the life of the last surviving author and [-fifty-]{+70+} years
after such last surviving author's death.

(c) Anonymous Works, Pseudonymous Works, and Works Made for Hire.-
...a term of [-seventy-five-]{+95+} years from the year of its first
publication, or a term of [-one hundred-]{+120+} years from the year
of its creation, whichever expires first.

(e) Presumption as to Author's Death.-After a period of
[-seventy-five-]{+95+} years from the year of first publication...
or a period of [-one hundred-]{+120+} years from the year of its
creation...died less than [-fifty-]{+70+} years before, is entitled
to the benefits of a presumption that the author has been dead
for at least [-fifty-]{+70+} years.
```

*Example reworked thanks to [this discussion](https://bsky.app/profile/questauthority.bsky.social/post/3mje3zpeyfo2p) ([continuation](https://bsky.app/profile/questauthority.bsky.social/post/3mje3zpeyfp2p)) and [this critique](https://bsky.app/profile/stzeitouni.bsky.social/post/3mjejrkftkc2f).*