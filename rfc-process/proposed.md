# Proposed RFCs

## Contents

- [Module Federation Host-Remote Contract](#module-federation-host-remote-contract)

### Module Federation Host-Remote Contract

[Link](https://billcom.atlassian.net/wiki/spaces/ACP/pages/3058761975/Migrating+Stardust+to+Hexagonal+Architecture)

#### Definitions

1. Host application - The application loading the single-spa Application or Parcel
2. Remote application - The single-spa Application or Parcel being loaded by
   module federation

#### Recommendation

A previous RFC requires all components be wrapped in a single-spa
[Parcel](https://single-spa.js.org/docs/parcels-overview/). This RFC recommends
the following approach:

- Parcel props
  - MUST be framework agnostic
  - MUST be trivial for a host to construct, or have construction thoroughly
    documented in the Remote Application’s repository
  - MUST be of type Constant, State, Callback, v3 ApolloClient
  - MUST have defined TS types if the codebase is written in TS
  - Published deprecation policy in "remote" repo that adhere's to this RFCs
    deprecation policy

- Host Applications:
  - MUST share all dependencies at runtime via Module Federation
  - MUST use pathfinder to provide themes via global CSS variables

- Remote Application or Parcel dependencies shared at runtime via module federation
  - MUST use these global CSS variables for theming
  - MUST not use `singleton: true` property
  - SHOULD share as many dependencies as possible via Module Federation
  - MAY opt to not share specific dependencies via Module Federation

- Remote and Host Applications MUST avoid sharing properties and dependencies
  outside of Parcel props and Module Federation
