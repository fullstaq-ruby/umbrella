# Fullstaq Ruby project roadmap

## Open

### Epic 4: Improve contributor friendliness for Server Edition

[![Server Edition issues](https://img.shields.io/github/milestones/progress/fullstaq-labs/fullstaq-ruby-server-edition/3?label=Server%20Edition%20issues)](https://github.com/fullstaq-labs/fullstaq-ruby-server-edition/milestone/3)
[![fullstaq-rbenv issues](https://img.shields.io/github/milestones/progress/fullstaq-labs/fullstaq-rbenv/1?label=fullstaq-rbenv%20issues)](https://github.com/fullstaq-labs/fullstaq-rbenv/milestone/1)

Fullstaq Ruby's [long-term vision](https://www.joyfulbikeshedding.com/blog/2020-05-15-why-fullstaq-ruby.html) is to become healthy open source project that can run on its own, and that survives and thrives even without the active input of its founders.

We need to set up the appropriate documentation, systems and processes to allow easily accepting contributions. We need to think about team formations, on- and offboarding, triage processes, and more.

### Epic 5: Server Edition general availability (leaving beta)

[![Server Edition issues](https://img.shields.io/github/milestones/progress/fullstaq-labs/fullstaq-ruby-server-edition/1?label=Server%20Edition%20issues)](https://github.com/fullstaq-labs/fullstaq-ruby-server-edition/milestone/1)
[![Umbrella issues](https://img.shields.io/github/milestones/progress/fullstaq-labs/fullstaq-ruby-umbrella/1?label=Umbrella%20issues)](https://github.com/fullstaq-labs/fullstaq-ruby-umbrella/milestone/1)

Miscellaneous polish is required to let the Server Edition enter General Availability status.

### Epic 6: Container Edition

This is going to be a fork of the official Ruby images by Docker Inc. We'll integrate [activatecontaineruid](https://github.com/fullstaq-labs/activatecontaineruid) to encourage running as non-root.

### Epic 7: Heroku Edition

Still need to figure out how this works. Maybe we need to fork the Ruby buildpack. Maybe we can even convince the Ruby buildpack maintainers to use our distribution by default.

## Closed

### Epic 3: CI/CD infrastructure

 * [Roadmap board](https://github.com/fullstaq-labs/fullstaq-ruby-umbrella/projects/2)

Have a CI/CD pipeline so that we can fully automate the release process, and so that building is fast. Each release generates 70+ packages (in the future maybe 100+) this needs to be massively parallelized.

### Epic 2: Epic 2: APT/YUM repository

 * [Roadmap board](https://github.com/fullstaq-labs/fullstaq-ruby-umbrella/projects/1)

We currently host the DEB and RPM packages as files in the Github release system, but this is not very user friendly. We should have a proper APT and YUM repository from which users can download packages, and to which we can publish newly built packages.

Points of attention:

 * Highly available, because users will depend on it for production installs.
 * Integration with a CDN so that everybody can download quickly.
 * Signed. 
   - We need to think about GPG key management.
 * An HTTP API endpoint, used for publishing newly built packages.
   - A future CI/CD pipeline can integrate with this.
   - Must be authenticated.
   - Must allow atomically publishing many packages at once.
 * Retain older package versions.
   - We need to think about backups and preventing accidental overwrites of older packages.
 * The Passenger APT, YUM and generic binaries repositories used 5 TB/mo at its peak. If we assume that Fullstaq Ruby will become popular then we should keep this order of magnitude of traffic in mind.
