<style>
:root {
    --r-heading1-size: 2em;
}

.reveal-viewport {
  background-image: none, url("https://hackmd.io/_uploads/By9eszf-ll.svg");
  background-position: top 10px left 10px, top 10px right 10px;
  background-size: 80em, 20%;
  background-repeat: no-repeat, no-repeat;
}
.reveal {
  font-size: 32px;
}

</style>

# Modern HPC-access alternatives
Viktor Rehnberg
Chalmers University of Technology

<p style="text-align: center;">
  <img src="https://hackmd.io/_uploads/SkXVMQzbge.jpg" alt="Futuristic looking user interface" style="width: 50%;">
</p>

---

## Me
- Digital Research Engineer AI/ML since 4 years
- Mainly support at NAISS AI/ML cluster "Alvis"
- Disclaimer: User of access tools, not developer

---

## The typical HPC-cluster
![generic_cluster_sketch](https://hackmd.io/_uploads/rJrloHzWeg.svg)

---

## HPC = terminal?
![HPC via terminal](https://hackmd.io/_uploads/H1AiRPx-ge.png)

---

## Overview
- [SSH and Xforward](#/5)
- [Remote desktops](#/6)
- [IDEs with remote access](#/7)
- [Remote GUIs over HTTP/websockets](#/8)
- [Web portals](#/9)
- [Tools for submitting jobs](#/10)

---

## SSH and Xforward
![X11-matlab](https://hackmd.io/_uploads/HJw_v_l-gg.jpg)

----

### What about Wayland?
- X to Wayland transition is here
- X deprecated/dropped in new/future clusters \[[1](https://access.redhat.com/documentation/en-us/red_hat_enterprise_linux/9/html/9.0_release_notes/deprecated_functionality#deprecated-functionality_graphics-infrastructures),[2](https://www.redhat.com/en/blog/rhel-10-plans-wayland-and-xorg-server)\]
- Wayland is not designed for remote graphics
- Changes will be needed (in many of the tools discussed today)

---

## Remote Desktops
- A (linux) desktop on log-in nodes
- ThinLinc most commonly used
    - Commercial, limited license
- [Demo](https://alvis2.c3se.chalmers.se:3000/)

----

### Launching graphical programs on compute nodes 
- [Gfxlauncher](https://gfxlauncher-documentation.readthedocs.io/en/latest/introduction.html)
    - Launches compute job and relevant connection

---

## IDEs with remote access
- Connect to remote via SSH
- Examples:
    - VSCode
    - PyCharm
    - Eclipse

---

## Remote GUIs over HTTP/Websockets
- Examples:
    - JupyterLab
    - RStudio Server
    - matlab-proxy
    - code-server
    - TensorBoard
- Demo:
```
ssh -L 11235:localhost:11235 vikren@alvis2.c3se.chalmers.se "ml JupyterLab && jupyter lab --port=11235"
```

---

## Web portals
- Open OnDemand
- [Demo](https://alvis.c3se.chalmers.se)

---

## Tools for submitting jobs
- submitit, Matlab, Nextflow
- Demo (JupyterLab)

---

## Implementation status in the HPC landscape
Typical availability:
 - X11 forwarding: Yes
 - Remote Desktops: ThinLinc (limited no. sessions)
 - Gfxlauncher: No
 - IDEs with remote access: Yes
 - Remote GUIs over HTTP: Yes
 - Webportal: No, but Open OnDemand gaining traction
 - Job-launchers: Yes (user installation)

---

### EuroHPC-JU
- Open OnDemand part of EuroHPC Federation Platform
- Has OpenOnDemand, but not ThinLinc
    - [LUMI](https://eurohpc-ju.europa.eu/supercomputers/our-supercomputers_en#lumi)
    - [Meluxina](https://eurohpc-ju.europa.eu/supercomputers/our-supercomputers_en#meluxina)
    - [Karolina](https://eurohpc-ju.europa.eu/supercomputers/our-supercomputers_en#karolina)
    - [Vega](https://eurohpc-ju.europa.eu/supercomputers/our-supercomputers_en#vega)
- Has Thinlinc, but not yet Open OnDemand
    - [Leonardo](https://eurohpc-ju.europa.eu/supercomputers/our-supercomputers_en#leonardo)
- Has both
    - [Deucalion](https://eurohpc-ju.europa.eu/supercomputers/our-supercomputers_en#deucalion)

---

### Sweden
- [Dardel](https://www.pdc.kth.se/hpc-services/computing-systems/dardel-hpc-system/dardel-1.1043529)
    - Has Gfxlauncher
- [Alvis](https://www.c3se.chalmers.se/about/Alvis/)
    - Has Open OnDemand
    - ThinLinc and alternative in beta (Apache Guacamole)
- [Bianca](https://www.uu.se/centrum/uppmax/resurser/kluster/bianca)
    - For sensitive data, much more locked down
- [Tetralith](https://www.nsc.liu.se/systems/tetralith/)
- [Berzelius](https://www.nsc.liu.se/systems/berzelius/)

---

### Denmark
- [DeiC Throughput HPC](https://www.deic.dk/en/supercomputing/national-hpc-facilities)
    - [Computerome 2.0](https://escience.sdu.dk/index.php/type-2-computerome/)
    - [GenomeDK](https://escience.sdu.dk/index.php/type-2-genomedk/)
    - [Sophia](https://escience.sdu.dk/index.php/type-2-sofia/)
    - No information
- [Hippo](https://docs.hpc-type3.sdu.dk/)
    - No remote desktop

---

### Finland
- [Puhti](https://research.csc.fi/service/puhti/)
- [Mahti](https://research.csc.fi/service/mahti/)
- Similar set-up on all CSC clusters
    - Open OnDemand
    - Not ThinLinc

---

### Norway
- [Betzy](https://documentation.sigma2.no/hpc_machines/betzy.html#betzy)
- [Fram](https://documentation.sigma2.no/hpc_machines/fram.html#fram)
- [Saga](https://documentation.sigma2.no/hpc_machines/saga.html#saga)
- Similar access on all NRIS clusters
    - Open OnDemand
    - X2Go remote desktops, not ThinLinc

---

### Iceland
- [Elja](https://irhpcwiki.hi.is/docs/Partitions/HPC-Elja/Elja/)
- [Mímír](https://irhpcwiki.hi.is/docs/Partitions/HPC-Mimir/Mimir/)
- [Jotunn](https://irhpcwiki.hi.is/docs/Partitions/HPC-Jotunn/Jotunn/)
- [Stefnir](https://irhpcwiki.hi.is/docs/Partitions/HPC-Stefnir/Stefnir/)
- No remote desktop access

---

## Can we stop writing jobscripts then?
- Not really

---

![Chalmers logotype + avancez-emblem, centered, black](https://hackmd.io/_uploads/Hkj_9nEble.png)
