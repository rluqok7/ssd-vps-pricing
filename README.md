# cloud computing services: types, real pricing, and how to pick a plan without bill shock

Search "cloud computing services" and you mostly get two things: glossary pages from hyperscalers explaining the term for the millionth time, or listicles ranking the same five names you already know. Neither answers the questions people actually have — what do these services concretely include, what do they cost per month, and which one fits the project sitting in front of you.

This guide takes a different route. Short on buzzwords, long on specifics: how the service types differ, how the pricing models really behave (including the egress-fee trap that ruins cloud budgets), and a complete, current plan comparison from Sharktech — an OpenStack-based provider we'll use as the worked example, since its pricing is published down to the hourly rate. By the end you should be able to pick a plan type with numbers in hand instead of vibes.

**What "cloud computing services" actually means**

Strip away the marketing and a cloud computing service is rented infrastructure: compute, storage, and networking delivered over the internet, billed by usage, and managed through a control panel or API instead of a data center contract.

The practical differences from owning hardware are the ones that matter:

- No upfront capital. You don't buy servers, racks, redundant power, or cooling — the provider already did.
- Deployment in minutes. A new virtual machine takes a few clicks instead of a procurement cycle.
- Elastic resources. CPU, RAM, and storage can scale up or down as workloads change, without reinstalling anything.
- Metered billing. You pay for what you provision or consume, which is either the best thing about cloud or the worst, depending on how well you understand the price sheet.

That last point deserves emphasis. Metered billing is where most bad cloud experiences come from — not from slow servers, but from invoices that don't match expectations. We'll come back to that with real numbers.

**The three service types: IaaS, PaaS, SaaS**

Nearly every article on this topic repeats the IaaS/PaaS/SaaS trio, so here it is once, in the version that actually helps you choose:

| Type | What you manage | Typical examples | Best for |
| --- | --- | --- | --- |
| IaaS (Infrastructure) | OS, runtime, apps — the provider handles hardware and virtualization | AWS EC2, Azure VMs, Sharktech Public Cloud | Full control, custom stacks, migrating existing servers |
| PaaS (Platform) | Just your code — the provider runs the runtime and build pipeline | App platforms, managed Kubernetes services | Developers who don't want to patch operating systems |
| SaaS (Software) | Nothing — you use finished software | Gmail, Office 365, Salesforce | End users, zero admin |

If you're comparing hosting plans or reading pricing pages, you're shopping in the IaaS layer. That's where Sharktech's core products live too: OpenStack-based Public and Dedicated Cloud, plus a managed Cloud Applications Platform that leans toward the PaaS side for people who'd rather not touch server config at all.

**Public cloud, dedicated cloud, VPS: the distinction that decides your bill**

Most confusion around cloud pricing comes from mixing up three deployment models. Sharktech's own product line happens to illustrate them cleanly, and the same logic applies to almost any provider:

- **Public cloud (pay-as-you-go pool).** You buy a pool of resources with an included monthly commit. Use more than the commit and the excess is billed hourly. Sharktech caps the maximum on its smaller tiers specifically so a runaway workload can't produce a runaway invoice — a detail worth checking on any provider, because not all of them do this.
- **Dedicated cloud (prepaid, fixed).** You pay a flat monthly price for an exact allocation. In Sharktech's words: pay for 8 cores, get 8 cores, no more, no less. Better economics for steady 24/7 workloads.
- **VPS (single slice).** One flat monthly fee for a fixed slice of a server. Cheapest entry point, fine for one or two small workloads, but you don't get the multi-VM flexibility of a resource pool.

The interesting part of Sharktech's setup is that Public and Dedicated Cloud run on the same OpenStack infrastructure — the difference is purely the billing model. That means you can start pay-as-you-go and move to prepaid commitments without re-architecting anything.

**How cloud pricing actually works — and where it goes wrong**

Three mechanisms determine what you'll pay on almost any IaaS platform.

*Included commits plus hourly overage.* A plan includes a baseline (say, 4 vCPUs and 8 GB RAM), and anything above it bills by the hour. On Sharktech's Small-to-Large public cloud tiers, the overage rates are $0.0025 per core-hour, $0.0035 per GB of RAM per hour, and storage at $0.00006/GB/hr for SSD, $0.00009/GB/hr for NVMe, and $0.00002/GB/hr for HDD. The Enterprise tier pays less per unit when it overflows: $0.002 per core-hour and $0.000045/GB/hr for SSD, for example. Extra IPv4 addresses are $1.50/month each after the first free one.

*The egress trap.* This is the line item nobody reads until the invoice arrives. Major hyperscalers charge around $0.09 per GB for outbound data at the entry tiers — AWS's first 10 TB per month is billed at that rate, Azure sits near $0.087/GB. Sharktech includes 20 TB of outgoing transfer on every public cloud tier, charges nothing for inbound, and bills overage at $0.002/GB. Run the math on one terabyte of excess outbound: roughly $90 at hyperscaler rates versus $2 here. If your workload pushes a lot of data out — media, CDN origins, API-heavy services — this single line decides the provider comparison.

*Resource caps versus uncapped tiers.* Uncapped resources are a feature when you're scaling fast and a liability when a script misbehaves. Sharktech caps Small through Large; Enterprise and Custom are uncapped with lower unit rates. Decide which failure mode you'd rather explain to your boss.

Sharktech's own pitch is at least 40% savings versus the hyperscalers — treat that as marketing until you price your actual workload, but the egress math above is the kind of concrete arithmetic that makes the claim plausible for transfer-heavy setups.

**The full plan lineup, with current prices**

Sharktech has been around since 2003, started as a DDoS-protection-first host, and now serves over 1,000 businesses across 73 countries from five data centers: Los Angeles, Las Vegas, Denver, Chicago, and Amsterdam. The cloud platform is OpenStack (Virtuozzo Hybrid Infrastructure underneath), which matters if you care about avoiding proprietary-API lock-in.

Here is every cloud plan currently shown on their pricing pages:

| Plan | vCPU (included – max) | RAM | SSD storage | Included transfer | Monthly price | Get it |
| --- | --- | --- | --- | --- | --- | --- |
| Public Cloud – Small | 4 – 16 | 8 – 32 GB | 300 – 2,400 GB | 20 TB | $39.00 | [ deploy the Small tier](https://portal.sharktech.net/aff.php?aff=1611&pid=602) |
| Public Cloud – Medium | 8 – 32 | 16 – 64 GB | 800 – 6,400 GB | 20 TB | $79.00 | [ configure the Medium plan](https://portal.sharktech.net/aff.php?aff=1611&pid=603) |
| Public Cloud – Large | 32 – 128 | 64 – 256 GB | 1,500 – 12,000 GB | 20 TB | $249.00 | [ set up a Large deployment](https://portal.sharktech.net/aff.php?aff=1611&pid=604) |
| Public Cloud – Enterprise | 64+ (uncapped) | 128 GB+ (uncapped) | 5,000 GB+ (uncapped) | 20 TB | $499.00 | [ configure the Enterprise tier](https://portal.sharktech.net/aff.php?aff=1611&pid=605) |
| Public Cloud – Custom | Custom | Custom | Custom | Custom | Sales quote | [ request a custom quote](https://bit.ly/SharKTech) |
| Dedicated Cloud (XS – 3XL) | 8 – 512 | 16 – 1,024 GB | SSD / HDD / NVMe mix | 5 – 300 TB | From $86.23 | [ compare Dedicated Cloud tiers](https://portal.sharktech.net/aff.php?aff=1611&gid=102) |

A few notes that make the table make sense:

- The "included – max" ranges aren't a typo. Each tier commits a baseline and allows bursting to the max at the hourly rates listed above. The Small tier, for instance, starts at 4 cores and 8 GB but can run up to 16 cores and 32 GB when you need it, then settle back.
- Hourly equivalents work out to roughly $0.061/hr on Small, $0.129/hr on Medium, $0.399/hr on Large, and $0.741/hr on Enterprise for the included allocation.
- The resource pool isn't one VM. You can carve an allocation across multiple virtual machines in any combination — one big instance, or several small ones, your call.
- Dedicated Cloud is the prepaid model with its own tier ladder (XS through 3XL) and cycle discounts: 5% quarterly, 10% semi-annually, 15% annually.
- Custom plans are quoted by the sales team for compute, storage, and network beyond the Enterprise tier.

For genuinely small projects, there's also Smart VPS — a separate Proxmox-based line from $7.95/month (2–128 vCPU, 4–256 GB RAM, 40 GB–2 TB NVMe across tiers), where annual billing takes 50% off, dropping the entry tier to $3.98/month equivalent. It's a single-slice product rather than a pool, but for one small workload it's the cheapest way onto the same network: [👉 try a Smart VPS from $7.95/mo](https://portal.sharktech.net/aff.php?aff=1611&gid=126).

**What's included beyond the raw specs**

The order pages list included services that many providers charge for separately: Kubernetes cluster deployment, load balancing, security policies (firewall groups), routing, and network management all ship with the cloud plans at no extra cost.

The platform details are worth knowing if you're technical:

- Full OpenStack REST APIs — Nova for compute, Cinder and Swift for storage, Neutron for networking, Keystone for identity — so Terraform-style automation works the way you'd expect.
- Official Linux cloud images updated weekly, plus the option to upload your own ISOs, qcow images, and cloud-init scripts.
- Private networking, virtual routers with NAT, floating IPs, IPv6, and a free integrated VPN for bridging cloud VMs to on-premises hardware.
- No vendor lock-in: you can download your VM disk images whenever you want, which makes offsite backup and future migration a non-event.
- Storage tiers you can mix per volume: NVMe at roughly 1.2 GB/s and 18,000 IOPS for databases and hot paths, SSD at ~350 MB/s for general work, HDD at ~120 MB/s for archives.
- Built-in DDoS protection on the network — consistent with the company's origin story as a DDoS-focused host, and a real consideration if you run game servers or anything that attracts traffic attacks.

There's also a cost calculator in the ordering flow that lets you stack VMs, storage, and OS choices and see the hourly/monthly total before committing anything. Use it — it's the difference between guessing and knowing.

**Matching a plan to your workload**

With the numbers on the table, the decision logic gets short:

- **Staging environment or tiny production app:** Small at $39/month, or Smart VPS at $7.95 if one VM is genuinely enough. Don't buy pools you won't split.
- **A handful of production services:** Medium ($79) or Large ($249). The pool model shines here — split 16 GB of RAM across a web VM, a database VM, and a utility box instead of paying for three separate servers.
- **Steady, predictable 24/7 workloads:** Dedicated Cloud. Prepaid fixed allocation plus up to 15% off for annual billing beats hourly rates when your usage never dips.
- **Fast-growing or spiky workloads:** Enterprise. Uncapped resources with discounted overage rates, $0.0015/GB egress, and 20 TB included.
- **Attack-prone workloads** (game servers, anything controversial enough to get flooded): a provider whose network filters DDoS by default beats bolting on a scrubbing service after the first incident.

One honest limitation: five regions, all in the US and Amsterdam. If your users are mostly in Asia or South America, the latency math may not work in your favor, and no pricing makes up for physics.

**Getting started: the actual flow**

There's no free trial, but hourly billing makes the entry cost nearly trial-sized — a test VM for an afternoon costs cents. The deployment path, as documented in third-party walkthroughs and the order flow itself:

1. Pick a tier and a location from the five data centers.
2. Adjust the resource sliders — cores, RAM, SSD/HDD/NVMe split. The order summary updates the hourly and monthly totals live.
3. Optionally add Acronis Cloud Backup (offered at checkout, around $4/month for entry-level protection).
4. Check out. Payment options run wider than most hosts: credit card, PayPal, wire transfer, Western Union, and Alipay.
5. Log into the Virtuozzo-based cloud panel, create VMs from the weekly-updated image library, attach storage, configure networks and security groups.

Upgrades happen without redeploying — you can move between tiers or resize resources while the environment stays up.

**The fine print worth knowing**

Three policies separate the adults from the brochures here:

- **No refunds.** Payments are non-refundable, including setup fees. Billing disputes raised within 30 days can result in account credit if resolved in your favor, but not cash back. Test small before committing large.
- **It's unmanaged.** You run the operating system and your stack; support covers infrastructure, network, and hardware, and it's available 24/7. If you want someone else patching your servers, look at their managed application platform instead.
- **Windows licensing is your problem.** Linux distributions are included; Windows Server requires bringing or buying a license.

None of this is unusual for infrastructure hosting, but all of it is worth knowing before rather than after checkout.

**What testers and customers report**

HostAdvice's 2026 expert review of the public cloud scored it 9.4/10 overall, with the details behind the number: CPU and memory benchmarks that held stable under stress, NVMe reads around 5 GB/s in their tests, ~10 Gbps network throughput on the VM they tested, and a support ticket answered in 39 minutes at 1 AM. Their conclusion leaned toward "capable and cost-effective for developers and SMBs who value transparency over brand-name hype," while noting the limited region list as the main weakness.

Trustpilot tells a smaller-sample, rougher story: 3.4 out of 5 across 13 reviews. The recent ones are positive — a user calling the yearly VPS pricing "probably the best deal on the market," another reporting roughly a year without downtime, a third running automation workflows on the cheapest VPS without issue. The negative reviews are worth reading too: a 2025 complaint about recurring PayPal charges after cancellation, and a 2022 data-loss report. Thirteen reviews is a thin base for strong conclusions either way, but the pattern — solid infrastructure and pricing, occasional billing and edge-case friction — is at least consistent across sources.

The company's own uptime claim is 99.999% on its triple-redundant platform. Treat SLA numbers from any provider as a floor to hold them to, not a promise to bank on.

**Quick answers to common questions**

*Is cloud cheaper than running my own servers?* For most small and mid-size businesses, yes — once you price hardware refresh cycles, power, cooling, and the person who has to babysit it all. For large steady workloads, on-prem or dedicated hardware can win again.

*What happens if I exceed my included resources?* Usage above the commit bills hourly at the published rates. On Small-to-Large tiers, a hard cap stops the meter; Enterprise and Custom are uncapped.

*Can I change plans later?* Yes — resources and tiers scale up or down without redeploying your VMs.

*Is there a minimum contract?* No. Monthly or hourly billing; Dedicated Cloud rewards longer commitments with 5–15% discounts.

*Can I run Windows?* Yes, with your own license. All the standard Linux distributions are included.

**The short version**

The cloud computing services market is bigger than three logos. If your workload fits the US/Amsterdam footprint and you're tired of hyperscaler egress fees and per-feature upsells, an OpenStack shop with published hourly rates and 20 TB of included transfer is worth a serious look: [👉 compare all of Sharktech's current cloud plans](https://bit.ly/SharKTech). Start small, watch the calculator, and scale only when the numbers say so.
