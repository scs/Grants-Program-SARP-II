# SARP - Software Design

- **Team Name:** Supercomputing Systems AG (SCS)
- **Payment Address:** 0xd24622311a22470353bd21d9bcd9e02ba0cfebbe (USDC)
- **[Level](https://github.com/w3f/Grants-Program/tree/master#level_slider-levels):** 2

## Project Overview :page_facing_up:

This is the follow up to our initial [research proposal](https://github.com/w3f/Grants-Program/blob/master/applications/sarp-basic-functionality.md), that we delivered [here](https://github.com/w3f/Grant-Milestone-Delivery/pull/880). The goal of this work package is to evaluate different software designs to implement a static code analysis on substrate pallets with MIRAI. Furthermore we want to investigate issues and bugs, we found in MIRAI in the previous work package.

### Overview

[Runtime Pallets](https://docs.substrate.io/learn/runtime-development/) are modules for writing the business logic of blockchains in [Substrate](https://github.com/paritytech/substrate) (a Rust framework for building blockchains). These are usually concise pieces of standalone code with relatively few dependencies and clear specifications, hence tractable targets for performing static analysis and verification. The code quality of a runtime pallet is crucial, as even minor defects can result in major exploits like DoS attacks or the stealing of funds by a malicious party. A static code analysis can help to automate the auditing processes and prevent introduction of defects throughout the software life-cycle.

Therefore we would like to develop a tool - SARP (Static Analysis tool for Runtime Pallets) to perform static analysis with reasonable soundness guarantees. In particular, we would like to target vunerability classes that are detectable using dataflow analysis techniques like *tag analysis* and *taint analysis*.

Our team has a good understanding of substrate and Rust. We are still getting started on the topic of static code analysis.

### Project Details

We will base our work on [MIRAI](https://github.com/facebookexperimental/MIRAI/) and extend it with checks on substrate pallets. For details see the [Development Roadmap](#development-roadmap-nut_and_bolt)

### Ecosystem Fit

The tool will help any team developing substrate pallets. It can further be integrated in the CI pipelines of the teams, providing a continuous quality check on the pallet code.

In the long term it could be interesting to connect the work done here with the new emerging auditing DAOs (like [QRUCIAL DAO](https://github.com/w3f/Grants-Program/blob/master/applications/QRUCIAL_DAO.md)).


## Team :busts_in_silhouette:

### Team members

- Sabine Proll: Project Lead & Developer
- Thomas Niederberger: Developer
- Bigna Härdi: Developer
- Edith Chevrier: Developer

### Contact

- **Contact Name:** Sabine Proll
- **Contact Email:** Sabine.Proll@scs.ch | info@scs.ch
- **Website:** https://www.scs.ch

### Legal Structure

- **Registered Address:** Technoparkstrasse 1, 8005 Zürich, Switzerland
- **Registered Legal Entity:** Supercomputing Systems AG

### Team's experience

Supercomputing Systems AG is a contractor with 130 engineers, working in the fields of software, electronics and system design. Profound know-how, solid methodological competence as well as efficient project management are the foundation of our success. Within the company we have a team of 5 blockchain developers, who have experience in the Polkadot ecosystem.

Our blockchain team has been a contributor to the ecoysystem since 2019. We started with grants from the Web3 Foundation to build the basis for [Integritee](https://github.com/integritee-network) (see our grants from waves [1](https://github.com/w3f/General-Grants-Program/blob/master/grants/speculative/substrate_sgx_proposal.md), [3](https://github.com/w3f/General-Grants-Program/blob/master/grants/speculative/substrate-api-client.md) and [5](https://github.com/w3f/General-Grants-Program/blob/master/grants/speculative/SubstraTEE-extension-pack1.md)). After that, our team has worked for Integritee and Encointer as a contractor. Recently the team received grants from the Kusama treasury for maintaining and improving the [substrate-api-client](https://github.com/scs/substrate-api-client), see our proposals for [Nov 22 - Jan 23](https://kusama.subsquare.io/referenda/referendum/26) and [Feb 23 - Apr 23](https://kusama.subsquare.io/referenda/referendum/88), [May 23 - Jul 23](https://kusama.polkassembly.io/referenda/182). Also, we successfully delivered the [first milestone for SARP](https://github.com/w3f/Grant-Milestone-Delivery/pull/880).

### Team Code Repos

The team has mainly worked on the following repositories

- [SARP - Milestone 1 delivery](https://github.com/scs/MIRAI/tree/Milestone1_Research/substrate-examples)
- [Substrate Api Client](https://github.com/scs/substrate-api-client)
- [Integritee Worker](https://github.com/integritee-network/worker)
- [Encointer Sidechain](https://github.com/encointer/community-sidechain)

Github accounts of the team members

- https://github.com/masapr
- https://github.com/haerdib
- https://github.com/echevrier
- https://github.com/Niederb


### Team LinkedIn Profiles

- https://www.linkedin.com/in/sabine-proll-5a7118153
- https://www.linkedin.com/in/bigna-h%C3%A4rdi-736bb21a9
- https://www.linkedin.com/in/edith-chevrier-90233297
- https://www.linkedin.com/in/thomas-niederberger-6057b71a7

## Development Status :open_book:

In a first research project we investigated, if MIRAI can be used for static code analysis of substrate pallets. For this we did a proof of concept on two cases: 
- Check of [incorrect origin](https://github.com/scs/MIRAI/blob/Milestone1_Research/substrate-examples/pallet_template/README.md) in the [substrate node template](https://github.com/substrate-developer-hub/substrate-node-template/tree/e0c480c0f322d0b0d1b310c93fa646fc0cfdd2df/pallets/template)
- Validation of [unsigned transactions](https://github.com/scs/MIRAI/blob/Milestone1_Research/substrate-examples/offchain-worker/README.md) for substrate's [offchain worker example](https://github.com/paritytech/substrate/tree/ea9ce4c0af36310c0b0db264ab12cf4766b83750/frame/examples/offchain-worker)

The overall conclusion was, that it is best to run the analysis only on the newly written pallet code, but not on the code generated by substrate's macros. To facilitate this a detailed analysis of different software designs has to be evaluated.


The full documentation of our findings can be found [here](https://github.com/scs/MIRAI/tree/Milestone1_Research/substrate-examples).


## Development Roadmap :nut_and_bolt:



### Overview

- **Estimated duration:** 1 month
- **FTE:**  1
- **Costs:** 30,000 USD

### Milestone 1 Software Design & Bug Fixes

- **Estimated duration:** 1 month
- **FTE:**  1
- **Costs:** 30,000 USD

In our previous work, we found the following problems:

1. **Crashes and timeouts of MIRAI** Certain pieces of substrate code lead to crashes of MIRAI. In other cases, parts of the code are not analyzed/do not produce warnings, because MIRAI runs into a timeout before reaching this code. Because of this, our examples are rather simple and we couldn't add and check tags at the locations we originally wanted to.

2. **Complexity due to substrate macros** The main reason for crashes and timeouts in our examples, was caused by substrate macros, adding a lot of complexity to the code in the background. Ideally SARP only analyzes the newly written code of a pallet.

3. **Invasiveness of tag analysis** The code we wrote in our PoC is very invasive and changes the code of the pallet. This is not practical for end-users. Ideally the user doesn't need to change anything on their code, or at least the changes should be very simple.

To address 2. and 3. we plan to evaluate different software designs. These will be part of our deliverables and we plan to discuss these with Parity and/or Web3 Foundation.

To address 1. we want to further analyze timeouts and crashes in MIRAI. Possibly they can be resolved by bugfixes in MIRAI. If not, we need to find workarounds.


#### Deliverables

| Number | Deliverable                  | Specification                                                                                                                                                  | 
|--------|------------------------------|----------------------------------------------------------------------------------------------------------------------------------------------------------------|
| 0a.    | License                      | MIT                                                                                                                                                            |
| 0b.    | User Documentation           | We will provide a basic **tutorial** that explains how to reproduce our examples.                                                                              |
| 0c.    | Testing and Testing Guide    | We will provide a testing guide on how to run SARP with the different software designs. These might be on different branches of the repository.                |
| 1.     | Prototype Code               | Prototype code to showcase the different software designs.                                                                                                     | 
| 2.     | Documentation                | Technical documentation describing the different variants of software design and its implications to pallet developers.                                        | 
| 3.     | Engagement                   | We will discuss the different solutions and their implications with Web3 Foundation and/or Parity.                                                             |
| 4.     | Bug reports and PRs in MIRAI | Any issues or bugfixes in MIRAI will be reported as an issue, resp. provided as a PR in the [MIRAI repository](https://github.com/facebookexperimental/MIRAI). |






## Future Plans


1. Decide on vulnerabilities for an MVP. 
</br> For this we plan to engage with Web3 Foundation / Parity and auditing companies such as [OtterSec](https://osec.io/) or [FYEO](https://www.fyeo.io/).
2. Implement a first simple version of the tool, together with tests and documentation. 
3. Improve the usability, by providing
   * means to surpress warnings
   * a comprehensive user tutorial, incl. documentation on the risks of each vulnerability
4. Add more features including checks on more vulnerability classes.

Once we have a tool with a good feature set and basic usability features, we want to further promote it to auditors and developers.


## Additional Information :heavy_plus_sign:

With our work in the previous grant, we deliberately invested into this project, as static code analysis was not our area of expertise. Our investment was two-fold: we used a lower hourly rate to calculate the cost and put in more effort than planned when implementing the project. With this package we increased the hourly rate and plan to stick closer to the estimated work effort.