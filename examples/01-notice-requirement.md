# Example 1: What was the law at time X?

## Where this question matters

Although this project is about copyright, "What was the law at time X" can be applied to other fields where legal status is determined by the statute as of a specific historical date:

> Fwiw, “what was the law at time X” is frequently important in immigration law (e.g., whether you have statutory birthright citizenship is dependent on the law as it existed on the date of your birth)
>
> — @jonweinberg.bsky.social, Apr 13, 2026, 09:45 PT — [link](https://bsky.app/profile/jonweinberg.bsky.social/post/3mjfcuzoakk2u)

> L1, in an citizenship law database, would also be incredibly useful for US citizenship determinations. Especially for children born outside of the US.
>
> — @an-elk.bsky.social, Apr 12, 2026, 23:39 PT — [link](https://bsky.app/profile/an-elk.bsky.social/post/3mjeaz2szls2n)

Copyright has its own version of this question. Notice requirements, renewal rules, and statutory duration are all anchored to publication and creation dates that can reach back decades, if the statute of limitations doesn't apply. The mechanic demonstrated below, using git to check out the statute as it stood at a specific moment, is the same regardless of what body of law the repository contains.

Similar tools exist: Westlaw's History tab (historical US Code from 1990, starting around $133/month for a solo-attorney single-state subscription) and HeinOnline (historical US Code from 1925, subscription pricing quote-based). This repository has every act back to 1790 and is free.

## Scenario

A publisher is evaluating reissue rights for a 1985 illustrated book. One of the photographs was published without a copyright notice. Is it in the public domain?

## Step 1: Find the relevant commits

```
$ git log --oneline -- sections/401.md
62e4f6d Berne Convention Implementation Act of 1988
6d717db Copyright Act of 1976
```

Two acts have amended Section 401: the 1976 Copyright Act and the Berne Convention Implementation Act of 1988. The exact commit hashes shown above will change every time the copyright repository is rebuilt — when you run this command in your own clone, you will see different short hashes. The commit messages and the ordering are stable; substitute your own hashes into the commands in Steps 2 and 3.

A work published in 1985 was governed by the original 1976 version of §401, in effect from January 1, 1978 (the 1976 Copyright Act's effective date) until the Berne Act took effect on March 1, 1989. Works published before January 1, 1978 were governed by the 1909 Act's notice regime, which is not the same analysis.

## Step 2: Read the law as it existed before the 1988 amendment

```
git show 62e4f6d~1:sections/401.md
```

This outputs the text of Section 401 as it stood between 1976 and 1988:

> §401. Notice of copyright: Visually perceptible copies
>
> (a) **General Requirement.**—Whenever a work protected under this title is published in the United States or elsewhere by authority of the copyright owner, a notice of copyright as provided by this section **shall be placed on all publicly distributed copies** from which the work can be visually perceived, either directly or with the aid of a machine or device.

Notice was mandatory: "shall be placed on all."

## Step 3: See what the 1988 Berne Convention Act changed

```
git diff 62e4f6d~1 62e4f6d -- sections/401.md
```

The substantive changes:

```diff
-(a) General Requirement.-Whenever a work protected under this title is
-published in the United States or elsewhere by authority of the copyright
-owner, a notice of copyright as provided by this section shall be placed
-on all publicly distributed copies
+(a) General Provisions.-Whenever a work protected under this title is
+published in the United States or elsewhere by authority of the copyright
+owner, a notice of copyright as provided by this section may be placed
+on publicly distributed copies
```

```diff
-(b) Form of Notice.-The notice appearing on the copies shall consist of
-the following three elements:
+(b) Form of Notice.-If a notice appears on the copies, it shall consist of
+the following three elements:
```

```diff
+(d) Evidentiary Weight of Notice.-If a notice of copyright in the form and
+position specified by this section appears on the published copy or copies
+to which a defendant in a copyright infringement suit had access, then no
+weight shall be given to such a defendant's interposition of a defense
+based on innocent infringement in mitigation of actual or statutory damages,
+except as provided in the last sentence of section 504(c)(2).
```

What the Berne Convention Implementation Act did to §401:

- "General Requirement" → "General Provisions"
- "**shall** be placed on **all** publicly distributed copies" → "**may** be placed on publicly distributed copies" — notice became optional
- "The notice appearing on the copies shall consist of" → "If a notice appears on the copies, it shall consist of" — a conditional tense change reflecting that notice was no longer required
- **Added** subsection (d) on evidentiary weight — foreclosing the innocent-infringement defense as a damages-mitigation argument when the defendant had access to a noticed copy, preserving one specific legal incentive to use notice even after notice itself became optional

Whether the missing notice actually placed the photograph in the public domain depends on §405's cure provisions — check `sections/405.md` at the same commit for that analysis.

---

*Example reworked thanks to [this discussion](https://bsky.app/profile/questauthority.bsky.social/post/3mje3zpeyfm2p) ([continuation](https://bsky.app/profile/questauthority.bsky.social/post/3mje3zpeyfn2p)) and [this critique](https://bsky.app/profile/stzeitouni.bsky.social/post/3mjejrkftkc2f).*

## Sources

- [Copyright Act of 1976 — Wikipedia](https://en.wikipedia.org/wiki/Copyright_Act_of_1976) — Oct 19, 1976 signing, Jan 1, 1978 effective date for most provisions
- [Timeline 1950–1997 — U.S. Copyright Office](https://www.copyright.gov/timeline/timeline_1950-1997.html)
- [Copyright Law / Copyright Formalities — Wiki Law School](https://www.wikilawschool.org/wiki/Copyright_Law/Copyright_Formalities) — Jan 1978 – Feb 1989 mandatory-notice regime and §405 cure provisions
- [17 U.S.C. § 401 — Cornell LII](https://www.law.cornell.edu/uscode/text/17/401)
- [17 U.S.C. § 507 — Cornell LII](https://www.law.cornell.edu/uscode/text/17/507)
- [Supreme Court Clarifies That Copyright Damages Are Not Limited to Three Years — Skadden, May 2024](https://www.skadden.com/insights/publications/2024/05/supreme-court-clarifies-that-copyright-damages-are-not-limited-to-three-years)
- [Prior Versions — Boston College Law Library](https://lawguides.bc.edu/statutes/priorversions) — Westlaw historical US Code begins in 1990
- [Westlaw Edge Pricing — Lawyerist 2026 review](https://lawyerist.com/reviews/online-legal-research/westlaw/) — solo-attorney single-state subscription starting price
