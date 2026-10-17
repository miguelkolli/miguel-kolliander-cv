# MGnarf

## Public fail-closed execution gate for AI-assisted and automated work

**Status:** 🟢 Public / live  
**Stable release:** `v1.70`  
**Repository:** https://github.com/miguelkolli/mgnarf  
**License:** Apache License 2.0

MGnarf on rakentamani avoimen lähdekoodin execution gate, jonka tarkoitus on erottaa AI:n tai automaation tuottama työ siitä auktoriteetista, joka saa tehdä oikean vaikutuksen ulkomaailmaan.

Yksinkertainen malli:

```text
AI / automation
      |
      v
produces candidate
      |
      v
verification / tests
      |
      v
    MGNARF
      |
      v
real effect
```

Esimerkiksi testien aikaisempi PASS ei yksin riitä deployn, tietokantamuutoksen tai muun suojatun toiminnon luvaksi. MGnarf sitoo evidencen täsmälliseen jäädytettyyn kandidaattiin ja tarkistaa auktoriteetin uudelleen ennen vaikutusta.

## Core ideas

- exact task, candidate, requirement, policy and effect binding
- authenticated verifier receipts
- dynamic `N/N` evidence coverage
- fail-closed handling of missing, stale, invalid or mismatched evidence
- immediate pre-effect state and revocation revalidation
- single-use protected effect admission
- optional identity and trust-domain separation
- authenticated causal stage ordering
- stable semantic operation identity across retries
- fencing for stronger execution paths
- PostgreSQL reference path for commit-time authority/fence validation

## Why I built it

AI-agentit voivat tehdä paljon työtä nopeasti, mutta tekninen ongelma ei ole vain se, osaako agentti tuottaa hyvän vastauksen tai läpäistä testin.

Vaikeampi kysymys on:

> **Onko juuri se työ, joka tarkistettiin, edelleen se työ joka on menossa tekemään oikean vaikutuksen — ja onko lupa edelleen voimassa juuri sillä hetkellä?**

MGnarf tekee tästä erillisen, eksplisiittisen portin.

## Security approach

MGnarf ei käsittele AI:n omaa väitettä, telemetriaa tai verifier-nimeä automaattisesti auktoriteettina. Trusted host omistaa verifier-valinnan, evidencen autentikoinnin, state/revocation-probet sekä suojatun effect credentialin.

Vahvemmat opt-in-polut lisäävät erikseen:

```text
identity separation
  -> authenticated stage order
  -> monotonic authority revision
  -> stable operation identity
  -> fencing
  -> target-side commit enforcement
```

Projektissa pidetään myös rajat näkyvinä. Esimerkiksi tokenin kuljettaminen ulkoiselle järjestelmälle ei vielä todista, että ulkoinen järjestelmä todella enforceaa sen commit-hetkellä.

## Verification and engineering work

Repository sisältää Python-reference implementationin, unit/adversarial-testit, Linux/UID-eristysmittauksia, rollback- ja crash-boundary testejä, PostgreSQL-authority/fencing-polkuja sekä GitHub Actions -evidenceä.

Työssä olen joutunut käsittelemään muun muassa:

- security boundary design
- authenticated evidence schemas
- replay and rollback threat models
- concurrency and causal ordering
- fail-closed API behavior
- TOCTOU boundaries
- PostgreSQL transactional fencing
- GitHub Actions release verification
- immutable release evidence
- public technical documentation

## Scope discipline

MGnarf ei väitä:

- että verifier olisi aina oikeassa
- että eri nimiset AI-agentit olisivat automaattisesti riippumattomia
- että kaikki ulkoiset API:t tarjoaisivat exactly-once-semanticsin
- että yksi paikallinen PASS poistaisi kaikki TOCTOU-ongelmat
- riippumatonta ulkoista turvallisuussertifiointia

Julkaistut väitteet sidotaan repositoryssa mitattuihin polkuihin ja dokumentoituihin rajoihin.

## Skills demonstrated

`Python` `Security Engineering` `AI Governance` `GitHub Actions` `Adversarial Testing` `Authentication` `Concurrency` `PostgreSQL` `Fencing` `Threat Modeling` `Technical Documentation`

## Links

- Public repository: https://github.com/miguelkolli/mgnarf
- Current stable release: https://github.com/miguelkolli/mgnarf/releases/tag/v1.70
- Documentation: https://github.com/miguelkolli/mgnarf/tree/main/docs
