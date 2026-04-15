# Example 4: Auditing a Section That's Been Amended Six Times

**Scenario**: A policy staffer wants to see every act that has touched §506 (criminal copyright offenses) and what each one changed in the *text*. This is step 1 of legislative-history research. What the changes *mean* — how courts have read them, how §506 interacts with the cross-referenced provisions in Title 18 — is not a question the repository answers. Committee reports, case law, and secondary sources are the next stop.

## Step 1: List every act that amended §506

```
$ git log --oneline -- sections/506.md
82a8c9a Prioritizing Resources and Organization for Intellectual Property Act of 2008 (PRO-IP Act)
1f5a98f Family Entertainment and Copyright Act of 2005
f470ca7 No Electronic Theft Act of 1997 (NET Act)
f12a20b Visual Artists Rights Act of 1990 (VARA)
c9ad8e2 Piracy and Counterfeiting Amendments Act of 1982
6d717db Copyright Act of 1976
```

Six commits since 1976. As with the other examples, the exact short hashes will differ in your clone — the commit messages and order are stable; substitute your own hashes into the commands below.

## Step 2: Read the 1976 original

```
$ git show v1976:sections/506.md
```

The original §506(a) has a default penalty plus a "Provided, however" clause with enhanced penalties for sound recordings and motion pictures:

> (a) Criminal Infringement.-Any person who infringes a copyright willfully and for purposes of commercial advantage or private financial gain shall be fined not more than $10,000 or imprisoned for not more than one year, or both: Provided, however, That any person who infringes willfully and for purposes of commercial advantage or private financial gain the copyright in a sound recording ... or the copyright in a motion picture ... shall be fined not more than $25,000 or imprisoned for not more than one year, or both, for the first such offense and shall be fined not more than $50,000 or imprisoned for not more than two years, or both, for any subsequent offense.

## Step 3: What each subsequent act changed

### 1982 — Piracy and Counterfeiting Amendments Act (PL 97-180)

The replacement text is much shorter than what it replaces, so a plain unified diff reads more clearly than a word-diff:

```
$ git diff c9ad8e2~1 c9ad8e2 -- sections/506.md
```

```diff
-(a) Criminal Infringement.-Any person who infringes a copyright willfully and for purposes of commercial advantage or private financial gain shall be fined not more than $10,000 or imprisoned for not more than one year, or both: Provided, however, That any person who infringes willfully and for purposes of commercial advantage or private financial gain the copyright in a sound recording afforded by subsections (1), (2), or (3) of section 106 or the copyright in a motion picture afforded by subsections (1), (3), or (4) of section 106 shall be fined not more than $25,000 or imprisoned for not more than one year, or both, for the first such offense and shall be fined not more than $50,000 or imprisoned for not more than two years, or both, for any subsequent offense.
+(a) Criminal Infringement.-Any person who infringes a copyright willfully and for purposes of commercial advantage or private financial gain shall be punished as provided in section 2319 of title 18.
```

Every dollar amount and sentence length in §506(a) is struck; the replacement is a cross-reference into Title 18.

### 1990 — Visual Artists Rights Act (PL 101-650, Title VI)

```
$ git diff --word-diff f12a20b~1 f12a20b -- sections/506.md
```

```
(e) False Representation.-Any person who knowingly makes a false
representation of a material fact in the application for copyright
registration provided for by section 409, or in any written statement
filed in connection with the application, shall be fined not more
than $2,500.
{+(f) Rights of Attribution and Integrity.-Nothing in this section
applies to infringement of the rights conferred by section 106A(a).+}
```

A single subsection is appended at the end. Nothing above is touched.

(Note: PL 101-650 was an omnibus containing both VARA and the Computer Software Rental Amendments Act, in different titles. The §506 change came from the VARA title.)

### 1997 — No Electronic Theft Act (PL 105-147)

```
$ git diff --word-diff f470ca7~1 f470ca7 -- sections/506.md
```

```
(a) Criminal Infringement.-Any person who infringes a copyright
willfully [-and-]{+either-+}
{+(1)+} for purposes of commercial advantage or private financial
[-gain-]{+gain, or+}
{+(2) by the reproduction or distribution, including by electronic
means, during any 180-day period, of 1 or more copies or phonorecords
of 1 or more copyrighted works, which have a total retail value of
more than $1,000,+}
shall be punished as provided [-in-]{+under+} section 2319 of title
[-18.-]{+18, United States Code. For purposes of this subsection,
evidence of reproduction or distribution of a copyrighted work, by
itself, shall not be sufficient to establish willful infringement.+}
```

"And" becomes "either—", and a new clause (2) is inserted alongside the existing commercial-motive clause (now renumbered (1)).

### 2005 — Family Entertainment and Copyright Act (PL 109-9)

A structural rewrite — subsection (a) is broken out into nested (1)/(2)/(3) form. Word-diff becomes noisy here, so a plain unified diff is easier to read:

```
$ git diff 1f5a98f~1 1f5a98f -- sections/506.md
```

```diff
-(a) Criminal Infringement.-Any person who infringes a copyright willfully either-
-(1) for purposes of commercial advantage or private financial gain, or
-(2) by the reproduction or distribution, including by electronic means, during any 180-day period, of 1 or more copies or phonorecords of 1 or more copyrighted works, which have a total retail value of more than $1,000,
-shall be punished as provided under section 2319 of title 18, United States Code. For purposes of this subsection, evidence of reproduction or distribution of a copyrighted work, by itself, shall not be sufficient to establish willful infringement.
+(a) Criminal Infringement.-
+(1) In general.-Any person who willfully infringes a copyright shall be punished as provided under section 2319 of title 18, if the infringement was committed-
+(A) for purposes of commercial advantage or private financial gain;
+(B) by the reproduction or distribution, including by electronic means, during any 180–day period, of 1 or more copies or phonorecords of 1 or more copyrighted works, which have a total retail value of more than $1,000; or
+(C) by the distribution of a work being prepared for commercial distribution, by making it available on a computer network accessible to members of the public, if such person knew or should have known that the work was intended for commercial distribution.
+(2) Evidence.-For purposes of this subsection, evidence of reproduction or distribution of a copyrighted work, by itself, shall not be sufficient to establish willful infringement of a copyright.
+(3) Definition.-In this subsection, the term "work being prepared for commercial distribution" means-
+(A) a computer program, a musical work, a motion picture or other audiovisual work, or a sound recording, if, at the time of unauthorized distribution-
+(i) the copyright owner has a reasonable expectation of commercial distribution; and
+(ii) the copies or phonorecords of the work have not been commercially distributed; or
+(B) a motion picture, if, at the time of unauthorized distribution, the motion picture-
+(i) has been made available for viewing in a motion picture exhibition facility; and
+(ii) has not been made available in copies for sale to the general public in the United States in a format intended to permit viewing outside a motion picture exhibition facility.
```

The old (1)/(2) becomes (A)/(B); a new (C) appears; a numbered (2) Evidence clause and a (3) Definition clause are added.

### 2008 — PRO-IP Act (PL 110-403)

```
$ git diff 82a8c9a~1 82a8c9a -- sections/506.md
```

```diff
-(b) Forfeiture and Destruction.-When any person is convicted of any violation of subsection (a), the court in its judgment of conviction shall, in addition to the penalty therein prescribed, order the forfeiture and destruction or other disposition of all infringing copies or phonorecords and all implements, devices, or equipment used in the manufacture of such infringing copies or phonorecords.
+(b) Forfeiture, Destruction, and Restitution.-Forfeiture, destruction, and restitution relating to this section shall be subject to section 2323 of title 18, to the extent provided in that section, in addition to any other similar remedies provided by law.
```

Subsection (b) is entirely rewritten. The heading gains ", and Restitution"; the body becomes a cross-reference into Title 18.

## Summary

| Year | Act | Surface change to §506 |
|------|-----|---------|
| 1976 | Copyright Act | Enacted §506 |
| 1982 | Piracy and Counterfeiting Amendments | §506(a) penalty text replaced with cross-reference to 18 U.S.C. §2319 |
| 1990 | VARA | Added subsec (f) |
| 1997 | NET Act | §506(a) restructured; a second trigger clause added |
| 2005 | Family Entertainment Act | §506(a) re-nested as (1)/(2)/(3); third trigger added; definition subsection added |
| 2008 | PRO-IP Act | Subsec (b) rewritten as a cross-reference to 18 U.S.C. §2323 |

Each row is a commit. Each change is a diff. That's as far as this repository takes you.

---

*Example reworked thanks to [this discussion](https://bsky.app/profile/questauthority.bsky.social/post/3mje3zpeyfo2p) on treating `git log` on a section as step 1 of legislative-history research rather than a substitute for it.*

## Sources

- [17 U.S.C. § 506 — Cornell LII](https://www.law.cornell.edu/uscode/text/17/506) — current text and full list of amending Public Laws
- [Public Law 94-553 (Copyright Act of 1976) — U.S. Copyright Office PDF](https://www.copyright.gov/history/pl94-553.pdf) — original §506 at 90 Stat. 2586
- [Public Law 97-180 (Piracy and Counterfeiting Amendments Act of 1982) — govinfo](https://www.govinfo.gov/content/pkg/STATUTE-96/pdf/STATUTE-96-Pg91.pdf)
- [DOJ Justice Manual §1847 — Criminal Copyright Infringement (17 U.S.C. 506(a) and 18 U.S.C. 2319)](https://www.justice.gov/archives/jm/criminal-resource-manual-1847-criminal-copyright-infringement-17-usc-506a-and-18-usc-2319) — confirms 1982 substitution of §2319 cross-reference
- [Public Law 101-650 (Judicial Improvements Act of 1990) — Federal Judicial Center](https://www.fjc.gov/content/319334/public-law-101-650) — 8-title omnibus including VARA (Title VI), AWCPA (Title VII), Computer Software Rental Amendments (Title VIII)
- [Visual Artists Rights Act of 1990 — Wikipedia](https://en.wikipedia.org/wiki/Visual_Artists_Rights_Act) — Pub. L. 101-650 Title VI; §606 added §506(f)
- [Computer Software Rental Amendments Act of 1990 — Cornell LII Table of Popular Names](https://www.law.cornell.edu/topn/computer_software_rental_amendments_act_of_1990) — confirms it's Title VIII of PL 101-650, amending §109 not §506
- [Public Law 105-147 (NET Act) — Congress.gov](https://www.congress.gov/105/plaws/publ147/PLAW-105publ147.htm) — rewrote §506(a) to add the $1,000 / 180-day trigger
- [Public Law 109-9 (Family Entertainment and Copyright Act of 2005) — U.S. Copyright Office PDF](https://copyright.gov/legislation/pl109-9.pdf) — pre-release piracy provisions in Title I (Artist's Rights and Theft Prevention Act)
- [CRS Report RS22042 — The Family Entertainment and Copyright Act of 2005](https://www.everycrsreport.com/reports/RS22042.html) — overview of §506 changes
- [Public Law 110-403 (PRO-IP Act of 2008) — Congress.gov](https://www.congress.gov/110/plaws/publ403/PLAW-110publ403.htm) — rewrote §506(b); added 18 U.S.C. §2323
- [U.S. Copyright Office NewsNet Issue 354 — PRO-IP Act](https://www.copyright.gov/newsnet/2008/354.html)
