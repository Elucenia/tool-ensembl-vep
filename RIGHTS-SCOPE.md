# Rights and deployment scope

The MIT grant covers only the ELUCENIA-authored adapters, parsers, schemas, labels, test harness, CLI, server and documentation in this package. It does not license any provider algorithm, model binary, logo, third-party annotation, or private ELUCENIA portal/dashboard. No such UI, authentication, database, patient data or credentials are included.

This is a bounded official-API client, not a reimplementation or validation of the complete named provider. The provider computes the prediction/enrichment; our tests check request/response contracts, source identities, numerical formatting and selected consistency assertions. Clinical approval and professional language review have not been performed.

Public/synthetic research inputs only. Requests go to the named provider, and result exports contain the query and attribution. Do not submit identifying, patient or confidential data. The CLI requires an explicit --live option for network use; tests and default offline mode never call providers.

A deterministic provider lock directory is shared by all packages and the website/dashboard under the same OS account on one host: os.homedir()/.elucenia/research-provider-locks. ELUCENIA_RESEARCH_LOCK_DIRECTORY is an optional absolute override; use the same directory for all apps. This is not cross-host distributed coordination. Active PIDs are never evicted only because a lease expired; interrupted uncertain IEDB requests retain a conservative five-minute cooldown.

The standalone server binds only to 127.0.0.1 and has no account/session system. A production proxy must provide separately reviewed authentication, authorization, transport and privacy controls. No private dashboard authentication source is distributed here.

## Ensembl data

The Ensembl project disclaimer offers unrestricted use of Ensembl-generated data, acknowledges scientific limitations and distinguishes third-party data. This workflow uses release116 REST15.12 human GRCh38 sequence verification and VEP region consequence output. It does not bundle Ensembl/VEP binaries, plugins, third-party licensed annotations or clinical interpretation. Attribution/source release remains in every result. Only forward-strand single-nucleotide substitutions are supported; no silent GRCh37 conversion.

Policy: https://www.ensembl.org/info/about/legal/disclaimer.html
API: https://rest.ensembl.org/documentation/info/vep_region_post
