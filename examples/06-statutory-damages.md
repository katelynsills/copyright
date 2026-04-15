# Example 6: What Statutory Damages Were Available?

**Scenario**: A rights holder discovers that their work was infringed in 1990. They want to know what statutory damages were available under Section 504 at the time.

## Step 1: Find every act that amended Section 504

```
$ git log --oneline -- sections/504.md
df60b47 Copyright Cleanup, Clarification, and Corrections Act of 2010
446aeb2 Intellectual Property Protection and Courts Amendments Act of 2004
5261a9e Digital Theft Deterrence and Copyright Damages Improvement Act of 1999
df95154 Fairness in Music Licensing Act of 1998
685f6e6 Copyright Technical Amendments Act of 1997
62e4f6d (tag: v1988-berne) Berne Convention Implementation Act of 1988
6d717db (tag: v1976) Copyright Act of 1976
```

## Step 2: See the damages range after the Berne Convention Act

```
git show 62e4f6d:sections/504.md
```

The 1988 Berne Act doubled the original 1976 dollar figures. For a 1990 infringement, the statutory damages range was:

- **Minimum**: $500 per work
- **Maximum**: $20,000 per work
- **Willful infringement**: up to $100,000
- **Innocent infringement**: as low as $200

## Step 3: See how the 1999 Act changed the range

The Digital Theft Deterrence and Copyright Damages Improvement Act of 1999 (PL 106-160) is the amendment that raised the numbers to today's levels:

```
git diff 5261a9e~1 5261a9e -- sections/504.md
```

Key changes in the diff:

```diff
-in a sum of not less than $500 or more than $20,000 as the court considers just.
+in a sum of not less than $750 or more than $30,000 as the court considers just.
```

```diff
-may increase the award of statutory damages to a sum of not more than $100,000.
+may increase the award of statutory damages to a sum of not more than $150,000.
```

The minimum, the maximum, and the willful cap all went up. The innocent-infringement floor ($200) was not touched.

## The escalation at a glance

| Era | Effective | Min | Max | Willful Max | Innocent Min |
|-----|-----------|-----|-----|-------------|--------------|
| 1976 Act | Jan 1, 1978 | $250 | $10,000 | $50,000 | $100 |
| Berne | Mar 1, 1989 | $500 | $20,000 | $100,000 | $200 |
| DTDCDIA | Dec 9, 1999 | $750 | $30,000 | $150,000 | $200 |

## Sources

- [17 U.S.C. § 504 — Cornell LII](https://www.law.cornell.edu/uscode/text/17/504) — current text and full amendment history
- [Public Law 100-568 (Berne Convention Implementation Act of 1988) — govinfo](https://www.govinfo.gov/link/statute/102/2860) — Berne amendments to §504(c); effective Mar 1, 1989
- [Digital Theft Deterrence and Copyright Damages Improvement Act of 1999 — WIPO Lex](https://www.wipo.int/wipolex/en/legislation/details/15267)
- [Public Law 106-160 (Digital Theft Deterrence and Copyright Damages Improvement Act of 1999) — govinfo PDF](https://www.govinfo.gov/content/pkg/PLAW-106publ160/pdf/PLAW-106publ160.pdf) — $500→$750, $20,000→$30,000, $100,000→$150,000
- [TOPN: Digital Theft Deterrence and Copyright Damages Improvement Act of 1999 — Cornell LII](https://www.law.cornell.edu/topn/digital_theft_deterrence_and_copyright_damages_improvement_act_of_1999)
