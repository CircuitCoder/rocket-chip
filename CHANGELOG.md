
# Changelog

## Version 1.6.0

### Added
### Changed
### Fixed

## Version 1.5.0

### Added
### Changed
* AHPParameters and APBParameters:
  * `PROT_PRIVILEDGED` - This was a typo. It is now `PROT_PRIVILEGED`.
  * https://github.com/chipsalliance/rocket-chip/pull/2925
* Remove Object Model from Diplomacy https://github.com/chipsalliance/rocket-chip/pull/2967/


### Fixed
* assert HasFSDirty false (https://github.com/chipsalliance/rocket-chip/pull/2997)
* Prevent selection of both Embedded and Hypervior extensions (https://github.com/chipsalliance/rocket-chip/pull/2988)
* VSStatus is now read-only and dirty when RoCC is enabled https://github.com/chipsalliance/rocket-chip/pull/2984
* removed RegEnable explicit arguments in preparation for changes in Chisel 3.6 https://github.com/chipsalliance/rocket-chip/pull/2986
* Copy EICG wrapper from vsrc when using Clock Gate Model  https://github.com/chipsalliance/rocket-chip/pull/2969/


## Version 1.4.0

RC has undergone two years of development since the last version update. The changelog for this version of RC is non-extensive.
The changelog for this version is merely illustrative of the features added since the 1.2~1.3 releases. No API compatibility is guaranteed between minor version releases of RC.
Future versions of the changelog should follow the format here https://keepachangelog.com/en/1.0.0/

* Chisel 3.4.x and FIRRTL 1.4 compatible.
  * Rely on building from source by default https://github.com/chipsalliance/rocket-chip/pull/2617
  * bump to 3.4.0 and FIRRTL 1.4.0 https://github.com/chipsalliance/rocket-chip/pull/2694

* Verilator 4.028 compatible
  * https://github.com/chipsalliance/rocket-chip/pull/2377

* submodules
  * torture https://github.com/ucb-bar/riscv-torture/tree/77195ab12aefc373ca688e0a9c4d710c13191341
  * hardfloat https://github.com/ucb-bar/berkeley-hardfloat/tree/01904f99ed3ad26cdbe2876f638d63e30e7fecdc
  * cde https://github.com/chipsalliance/cde/tree/fd8df1105a92065425cd353b6855777e35bd79b4
  * if building from source for firrtl and chisel:
    * firrtl: https://github.com/chipsalliance/firrtl/tree/7756f8f9634b68a1375d2c2ca13abc5742234201
    * chisel: https://github.com/chipsalliance/chisel3/tree/58d38f9620e7e91e4668266686484073c0ba7d2e


* scala 2.12.10
* scalatest 3.2.0
* json4s-jackson 3.6.1

* [ResetSynchronizer][ClockGroupResetSynchronizer] add a pair of diplomatic reset synchronizers https://github.com/chipsalliance/rocket-chip/pull/2666
  * replaced IdentityNodes with AdapterNodes https://github.com/chipsalliance/rocket-chip/pull/2689

* make RC more tolerant to x-prop https://github.com/chipsalliance/rocket-chip/pull/2659

* [util][rotate] fix `rotate` for zero-width wires https://github.com/chipsalliance/rocket-chip/pull/2663

* [SimJTAG][SimDTM] fix a verilator bug due to delay statements https://github.com/chipsalliance/rocket-chip/pull/2635

* [notification] provide reset values for cease and wfi https://github.com/chipsalliance/rocket-chip/pull/2449
* [notification][CSR] Block wfi, halt, cease, and other valid signals during asynchronous reset https://github.com/chipsalliance/rocket-chip/pull/2611
  * trace.valid of CSR changed to async-reset delay https://github.com/chipsalliance/rocket-chip/pull/2613
* [notification][WFI] expose WFI from core https://github.com/chipsalliance/rocket-chip/pull/2315


* [PLIC] add support for PLIC elaboration even when nDevices == 0
  * https://github.com/chipsalliance/rocket-chip/pull/2351
* [PLIC] fix off-by-one for priority register description https://github.com/chipsalliance/rocket-chip/pull/2718

* [hartid]
  * fixed an issue where the Rocket core's placement would be impacted by non-constant hartid
    * https://github.com/chipsalliance/rocket-chip/pull/2432
  * add a diplomatic node for assigning hartid
    * https://github.com/chipsalliance/rocket-chip/pull/2447

* distinguish a supervisor mode that does not use MMU/VM https://github.com/chipsalliance/rocket-chip/pull/2422 #2499

* [HasTiles] add seipNode https://github.com/chipsalliance/rocket-chip/pull/2665

* [stage] Fix a bug where unserializable RocketTestSuiteAnnotations were being serialized
* [stage] Fix a bug where the desired output file name was being superseded by another phase
  * https://github.com/chipsalliance/rocket-chip/pull/2424
* [RocketChipStage] Remove emitVerilog, emitFirrtl, and emitChirrtl methods from RocketChipStage https://github.com/chipsalliance/rocket-chip/pull/2481
* [stage] expose Stage's `--target-dir` to Config https://github.com/chipsalliance/rocket-chip/pull/2725

* [Transforms][Lint] add `RenameDesiredNames` transform and `LintConflictingModuleNames` Lint rule https://github.com/chipsalliance/rocket-chip/pull/2452
  * also adds RenameModulesAspect that can be used to emit name overrides and a LintConflictingModuleNamesAspect to collect DesiredNameAnnotations to be checked by the lint pass.

* [ElaborationArtefactAnnotation] add `ElaborationArtefactAnnotation` - an API similar to `ElaborationArtefacts` #2727
  * this API is for assuring metadata has correct instance paths and signal names
  * allow renames to multiple targets for `MemoryPathToken` https://github.com/chipsalliance/rocket-chip/pull/2729


* [i$] fixed bug where cease signal was asserted before potential glitching in I$ clock finished. Add an assertion to cease signal.
  * https://github.com/chipsalliance/rocket-chip/pull/2419/
  * https://github.com/chipsalliance/rocket-chip/pull/2420/
  * https://github.com/chipsalliance/rocket-chip/pull/2456/

* [i$] fix ccover bug to cover all beats of D channel corruption https://github.com/chipsalliance/rocket-chip/pull/2755

* [d$] updates
  * fix elaboration with < 4 MiB of physical address space https://github.com/chipsalliance/rocket-chip/pull/2367
  * guarantee no-alloc accesses are ordered even if aliased https://github.com/chipsalliance/rocket-chip/pull/2358
  * [ecc] fixed a rare bug where under the right conditions stores to the same word resulted in one store detecting an error while the other does not
    * https://github.com/chipsalliance/rocket-chip/pull/2458
  * [HellaCache] introduce `subWordBits` param to support subbanking https://github.com/chipsalliance/rocket-chip/pull/2645
  * support specifying cache index when aliasing is possible https://github.com/chipsalliance/rocket-chip/pull/2697
    * https://github.com/chipsalliance/rocket-chip/pull/2730
  * reduce latency on inclusion and coherence misses by allowing D$ to voluntarily release (aka "noisy drop") cache lines https://github.com/chipsalliance/rocket-chip/pull/2696
    * follow-up to fix deadlock: https://github.com/chipsalliance/rocket-chip/pull/2714
    * follow-up to fix performance: https://github.com/chipsalliance/rocket-chip/pull/2739

* [Replacement][PseudoLRU] fix performance issue with PseudoLRU for replacements when number of ways is not a power of 2 https://github.com/chipsalliance/rocket-chip/pull/2493 #2498

* [Replacement][d$] configure replacement policy with parameter to indicate wheteher policy is used on a per-set basis or a global basis https://github.com/chipsalliance/rocket-chip/pull/2656

* [PTW]
  * replace round robin arbitration with static arbitration https://github.com/chipsalliance/rocket-chip/pull/2433
  * fixed a bug where an L2TLB write would almost always block the next L2TLB search
    * when MMU and clock gating were enabled https://github.com/chipsalliance/rocket-chip/pull/2601
  * wait for L2TLB to refill before searching https://github.com/chipsalliance/rocket-chip/pull/2619
  * [PTWPerfEvents] add (unused) Performance Monitor Events for L2TLB hit and PTE Cache Miss/Hit https://github.com/chipsalliance/rocket-chip/pull/2668 https://github.com/chipsalliance/rocket-chip/pull/2688 https://github.com/chipsalliance/rocket-chip/pull/2692
  * enable configurable set-associtive L2 TLB https://github.com/chipsalliance/rocket-chip/pull/2748
    * default configuration is direct-mapped
    * follow-up: fix x-prop bug https://github.com/chipsalliance/rocket-chip/pull/2753

* enable Sv48 setting page levels equal to 4
  * https://github.com/chipsalliance/rocket-chip/pull/2434

* [PMP] remove NA4 coverpoint for pmp granularity > 4 https://github.com/chipsalliance/rocket-chip/pull/2625

* [TLB]
  * check PutPartial support separately from PutFull https://github.com/chipsalliance/rocket-chip/pull/2503
  * fix a rare refill/invalidate race condition https://github.com/chipsalliance/rocket-chip/pull/2534
  * configure L1 D/I TLBs by set, entry, and replacement policy https://github.com/chipsalliance/rocket-chip/pull/2574 https://github.com/chipsalliance/rocket-chip/pull/2621


  * add params nTLBBasePageSectors and nTLBSuperpages for both I and D TLBs https://github.com/chipsalliance/rocket-chip/pull/2595

* Debug/DM:
  * mcontext and scontext CSRs for breakpoint qualification https://github.com/chipsalliance/rocket-chip/pull/2588/files
  * allow a fast debugger reading dmstatus in a single dminner clock cycle to read the proper value https://github.com/chipsalliance/rocket-chip/pull/2412
  * fix address sent from DM to SB2TL https://github.com/chipsalliance/rocket-chip/pull/2559
  * add bus blocker to deny requests to dmInner when dmactive = 0 https://github.com/chipsalliance/rocket-chip/pull/2205
  * DMIToTL: remove PutPartial https://github.com/chipsalliance/rocket-chip/pull/2598
  * convert registers and wires from a Regs of Vector to Regs of UInt https://github.com/chipsalliance/rocket-chip/pull/2597
  * make instantiation of reset synchronizers optional https://github.com/chipsalliance/rocket-chip/pull/2626
  * allow DM at base address other than 0 https://github.com/chipsalliance/rocket-chip/pull/2649
  * small tweaks:
    * [Periphery] workaround an autonaming bug with debug https://github.com/chipsalliance/rocket-chip/pull/2657
    * make `nExtTriggers` a val for compatibility with cloneType https://github.com/chipsalliance/rocket-chip/pull/2667/

* [OMMemoryMap] require register map to only go to one memory region https://github.com/chipsalliance/rocket-chip/pull/2496

* Object Model:
  * [OMErrorDevice] added to Object Model
    * https://github.com/chipsalliance/rocket-chip/pull/2410
    * https://github.com/chipsalliance/rocket-chip/pull/2411
  * added IdRange, IDMap to include source ids in object model #2495
  * added L2UTLB entries and memory https://github.com/chipsalliance/rocket-chip/pull/2606
  * [OMISA] Add OMVectorExtension.vstartALU field https://github.com/chipsalliance/rocket-chip/pull/2578

* [BuildInDevices] introduce case class parameters to Zero and Error device https://github.com/chipsalliance/rocket-chip/pull/2684
  * make instantiation of buffers optional
  * allow for optional instantiation of CacheCork

* [DTS] allow node names up to 48 bytes https://github.com/chipsalliance/rocket-chip/pull/2570

* [PMP][DTS] add pmp granularity to DTS https://github.com/chipsalliance/rocket-chip/pull/2661


* [RegFieldDesc]
  * add AddressBlocks for RegFieldDesc https://github.com/chipsalliance/rocket-chip/pull/2437
  * require RegFieldDesc to match RegEx to limit to a subspect of IP-XACT standard https://github.com/chipsalliance/rocket-chip/pull/2525

* [CSR] add vcsr and move vxrm/vxstat from fcsr to that register set
  * https://github.com/chipsalliance/rocket-chip/pull/2400
  * https://github.com/chipsalliance/rocket-chip/commit/71fd9b34a8ebafa05ccb6164c7bd8e26ec102957

* [CSR] disallow writes to MSTATUS.XS https://github.com/chipsalliance/rocket-chip/pull/2508
* [CSR] expand TracedInstruction.cause to xLen https://github.com/chipsalliance/rocket-chip/pull/2548
* [CSR][mstatus] implement updated MPRV from priv-1.12 https://github.com/chipsalliance/rocket-chip/pull/2206
* [CSR] add `mcountinhibit from priv-1.11 https://github.com/chipsalliance/rocket-chip/pull/2693
  * [RocketCore] ignore PAUSE when `mcountinhibit(0)` === 1 #2700


* add partial multiple reset scheme support https://github.com/chipsalliance/rocket-chip/pull/2375


* register coverage now generated based on access type https://github.com/chipsalliance/rocket-chip/pull/2384


* BundleMap: improved API for user bits
  * https://github.com/chipsalliance/rocket-chip/pull/2318
    * Customizable field unification, Default for bulk assignments, Field and Key class required
  * https://github.com/chipsalliance/rocket-chip/pull/2326
    * Use BundleMap for AMBA protocols
  * https://github.com/chipsalliance/rocket-chip/pull/2335
    * various bug fixes to TL user fields

* AMBA: combine modifiable and cacheable, add read and write alloc fields https://github.com/chipsalliance/rocket-chip/pull/2386


* CoreMonitor:
  * add privilege mode and exception signals https://github.com/chipsalliance/rocket-chip/pull/2387
  * now prints only retired instructions https://github.com/chipsalliance/rocket-chip/pull/2372
  * separate wren into wrenx/wrenf for integer/float https://github.com/chipsalliance/rocket-chip/pull/2423/
  * Add [CoreMonitorBundle] for [FPU] floating point registers https://github.com/chipsalliance/rocket-chip/pull/2538 https://github.com/chipsalliance/rocket-chip/pull/2541 https://github.com/chipsalliance/rocket-chip/pull/2546 https://github.com/chipsalliance/rocket-chip/pull/2589

* [FPU] Zfh extension, option for Half-Precision unit https://github.com/chipsalliance/rocket-chip/pull/2723
  * replaces `singleIn` and `singleOut` with `typeTagIn` and `typeTagOut`

* [BEU]
  * added a Device Tree description for the bus error unit https://github.com/chipsalliance/rocket-chip/pull/2373
  * report Corrupt+Denied on I-Fetch https://github.com/chipsalliance/rocket-chip/pull/2482

* add test enable pin to Clock Gate https://github.com/chipsalliance/rocket-chip/pull/2087

* compiler warning fixes #2357, #2356, #2355, #2354, #2353, #2378, #2379, #2380, #2442, #2567, #2757, #2758

* AsyncResetReg: use chisel3 async resets

* Async Reset support for Atomics, FPU, and TLBroadcast https://github.com/chipsalliance/rocket-chip/pull/2362

* preliminary RV32Zfh extension support https://github.com/chipsalliance/rocket-chip/pull/2359

* [ObjectModel] teach OM about Zfh extension https://github.com/chipsalliance/rocket-chip/pull/2581


* Make AsyncValidSync a RawModule https://github.com/chipsalliance/rocket-chip/pull/2352



* Synchronizer primitive changes https://github.com/chipsalliance/rocket-chip/pull/2212
  * introduction of `ClockCrossingReg`
  * _SynchronizerShiftReg requires synchronizer depth > 1
  * deprecate IntXing and IntSyncCrossingSink
  * deprecate SyncResetSynchronizerShiftReg

* [SynchronizerPrimitiveShiftReg] correct the dedup behavior for the *ResetSynchronizerPrimitiveShiftReg so you only end up with one copy https://github.com/chipsalliance/rocket-chip/pull/2547

* Comply with priv spec by resetting and initializing mcause to 0 https://github.com/chipsalliance/rocket-chip/pull/2333

* Events: Add SuperscalarEventSets
  * https://github.com/chipsalliance/rocket-chip/pull/2337
  * https://github.com/chipsalliance/rocket-chip/pull/2506
  * make event fields public for tapping signals
    * https://github.com/chipsalliance/rocket-chip/pull/2464
    * https://github.com/chipsalliance/rocket-chip/pull/2524


* fixed an issue where multiplierIO was unclonable https://github.com/chipsalliance/rocket-chip/pull/2331


* [Diplomacy]
  * versioning support https://github.com/chipsalliance/rocket-chip/pull/2320   <???>
  * allow users to access Lazy Module nodes https://github.com/chipsalliance/rocket-chip/pull/2301

  * JunctionNodes now support configurable up/down ratio
    * https://github.com/chipsalliance/rocket-chip/pull/2430

  * dynamic and remote order: fix QoR in designs with large physical address maps https://github.com/chipsalliance/rocket-chip/pull/2461

  * [AddressSet] fix a bug where duplicated AddressSets would cause incorrect widening when unify is called. #2502

  * [LazyModule]
    * mark LazyModules for inlining such as nodes with circuit identity (inputs are outputted unchanged) https://github.com/chipsalliance/rocket-chip/pull/2579
      * inline xbar patch: https://github.com/chipsalliance/rocket-chip/pull/2639
    * add scaladoc https://github.com/chipsalliance/rocket-chip/pull/2311

  * Added more debug info to node requires https://github.com/chipsalliance/rocket-chip/pull/2577

  * [Nodes] documentation for Nodes https://github.com/chipsalliance/rocket-chip/pull/2604

  * [Nodes] replace `bundleSafeNow` guard with `instantiated` guard https://github.com/chipsalliance/rocket-chip/pull/2680

  * tutorial for adder https://github.com/chipsalliance/rocket-chip/pull/2615

  * [aop][Select] add Select Library API #2674




* [RecordMap] addd as an API for better diplomatic IO naming https://github.com/chipsalliance/rocket-chip/pull/2486
  * used to get easier to follow Clock Group signal names https://github.com/chipsalliance/rocket-chip/pull/2528



* [AddressAdjuster] and RegionReplicator now work on prefixes (not chip id)
    * https://github.com/chipsalliance/rocket-chip/pull/2430
      * removes MultiChipMaskKey
* [AddressAdjuster] patches #2470
  * user can now supply a default local base address for reporting manager address metadata other than the 0th region
  * let local and remote legs have different user bits using <:= operator
  * allow for no fifo ordering on the replicated region
  * more verbose requires

* Topology changed from static traits to CDE-based configurable runtime https://github.com/chipsalliance/rocket-chip/pull/2327
  * `HasHierachicalBusTopology` trait replaced with two config options:
    * `WithCoherentBusTopology`
    * `WithIncoherentBusTopology`
* renamed attachment API to location API https://github.com/chipsalliance/rocket-chip/pull/2330

* [NMI] introduce non-maskable interrupt implementation https://github.com/chipsalliance/rocket-chip/pull/2711

* [InterruptBusWrapper] update synchronizer API https://github.com/chipsalliance/rocket-chip/pull/2640
  * replaces using `IntXing` in a `synchronize` method with `to` and `from` methods
  * this is to ensure synchronized registers are always put in the destination clock domain

* [BundleBridge] to propagate [TileInputConstants]. ROM attachment changes https://github.com/chipsalliance/rocket-chip/pull/2521 (merged as https://github.com/chipsalliance/rocket-chip/pull/2531)
  * `HasPeripheryBootROM` and `HasPeripheryBootROMModuleImp` are removed and replaced by a call to `BootROM.attach`
  * `BootROMParams` Field is removed and replaced with `BootROMLocated` Field
  * `MaskROMLocated` Field is added
  * `SubsystemExternalResetVectorKey`, `SubsystemExternalHartIdWidthKey` and `InsertTimingClosureRegistersOnHartIds` Fields are added
  * Unused `ResetVectorBits` Field is removed
  * `HasExternallyDrivenTileConstants` bundle mixin is removed
  * `HasResetVectorWire` subsystem trait is removed
  * `HasTileInputConstants` and `InstantiatesTiles` subsystem traits are added
  * `BaseTile` exposes `val hartIdNode: BundleBridgeNode[UInt]` and `resetVectorNode: BundleBridgeNode[UInt]` and these are automatically connected to in `HasTiles`.
  * `rocket.Frontend`, `rocket.ICache`, `rocket.DCache`, `rocket.NDCache` now have `BundleBridgeSink[UInt]` for their reset vector or hartid wire inputs.
    * If you instantiate them manually, i.e. not using the traits e.g. `rocket.HasHellaCache`, you will have to manually connect up those nodes to the aforementioned `BaseTile` nodes.
  * follow up PR - bug fix for HartID and ResetVector width calcluation https://github.com/chipsalliance/rocket-chip/pull/2543/

* Add an optional `TileInputConstant` as an MMIO Address Prefix used in ITIM and DTIM hit calculations  https://github.com/chipsalliance/rocket-chip/pull/2533
  * follow-up: fix traceCoreNode duplication issue https://github.com/chipsalliance/rocket-chip/pull/2561

* add HierarchicalLocation to LocationAPI https://github.com/chipsalliance/rocket-chip/pull/2346/

* `val tiles` in trait `HasTiles` is now populated eagerly via the `TilesLocated` Field. https://github.com/chipsalliance/rocket-chip/pull/2504

* [RocketCrossingParams] relax type of `master` param to `TilePortParamsLike` https://github.com/chipsalliance/rocket-chip/pull/2634/

* [Subsystem] Miscellaenous subsystem bus crossing changes https://github.com/chipsalliance/rocket-chip/pull/2724
  * introduce keys for bus crossings
  * allow for disabling of DriveClockFromMaster behavior
  * introduce MBus crossing to CoherentBusTopology

* [Subsystem][PLIC] avoid using implicit clock https://github.com/chipsalliance/rocket-chip/pull/2719

* [PRCI] wrap Tiles in PRCI Domains https://github.com/chipsalliance/rocket-chip/pull/2550
  * contains logic related to  power, reset, clock, and interrupt

* [PRCI] define `ResetCrossingType` and use with `BlockDuringReset` in `TilePRCIDomain` https://github.com/chipsalliance/rocket-chip/pull/2641/
  * analogous to `ClockCrossingType`. Currently, there are two crossing types: `NoResetCrossing` and `StretchedResetCrossing(cycles: Int)`
  * introduces `Blockable` util

* [ResetStretcher][PRCI] add reset stretcher for Async Reset systems https://github.com/chipsalliance/rocket-chip/pull/2566

* ClockGroupDriverParameters: allow for a configurable drive function for driving asynchronous clock groups with IO other than the implicit clock https://github.com/chipsalliance/rocket-chip/pull/2319

* [ClockDivider] fixed bug where clock divider's source and sink functions always divided by two https://github.com/chipsalliance/rocket-chip/pull/2610

* BPWatch: have the watchpoint compare to store or load instruction type for matching https://github.com/chipsalliance/rocket-chip/pull/2317

* [SCIE] fix width mismatch assignment lint warning from VCS https://github.com/chipsalliance/rocket-chip/pull/2563

* [IDPool] enable ResetAsynchronous Full https://github.com/chipsalliance/rocket-chip/pull/2568
* [IDPool] add `lateValid` and `revocableSelect` to shift the deep logic cones from before the `valid/selec` registers to after the `bitmap` register https://github.com/chipsalliance/rocket-chip/pull/2673 https://github.com/chipsalliance/rocket-chip/pull/2677
* [IDPool] infer widths https://github.com/chipsalliance/rocket-chip/pull/2679

* [RVV] -> 0.9 -> 1.0
  * #2477
    * Fractional LMUL
    * Tail-agnostic/mask-agnostic bits
    * EEW loads/stores
    * Some encoding changes
  * https://github.com/chipsalliance/rocket-chip/pull/2484
    * tighten fractional LMUL-SEW constraint
  * Instructions: add new RISC-V vector extension opcodes https://github.com/chipsalliance/rocket-chip/pull/2396/
    * VFSLIDE1UP_VF
    * VFSLIDE1DOWN_VF
    * VFCVT_RTZ_XU_F_V
    * VFCVT_RTZ_X_F_V
    * VFWCVT_RTZ_XU_F_V
    * VFWCVT_RTZ_X_F_V
    * VFNCVT_RTZ_XU_F_W
    * VFNCVT_RTZ_X_F_W
  * https://github.com/chipsalliance/rocket-chip/pull/2552
  * reorder fields in vtype https://github.com/chipsalliance/rocket-chip/pull/2576

* [Opcode][OM] add B extension opcodes and object model description https://github.com/chipsalliance/rocket-chip/pull/2678

* QoL
  * Initial scalatest flow support and aspect generation https://github.com/chipsalliance/rocket-chip/pull/2309/ https://github.com/chipsalliance/rocket-chip/pull/2517

  * [linting] add Chisel Linting Framework https://github.com/chipsalliance/rocket-chip/pull/2435

  * [scalafix] enable scalafix and remove unused imports https://github.com/chipsalliance/rocket-chip/pull/2648
    * This requires downstream projects using rocket-chip's build.sbt to enable scalafix.
    * enable LeakingImplicitClassVal https://github.com/chipsalliance/rocket-chip/pull/2650
    * enable ProcedureSyntax https://github.com/chipsalliance/rocket-chip/pull/2651

  * mdoc infrastructure https://github.com/chipsalliance/rocket-chip/pull/2615

  * [PlusArg]
    * support for no-default PlusArgs and string-valued PlusArgs #2453
    * fix VCS lint warning for plusarg default bit width: #2558, #2562

  * [FixChisel3] Added some scaladoc commentary to the operators :<>, :<=, :=> to explain what they do and the rationale for their creation. #2339

  * [util]
    * Add utilities for bitwise shifts by signed shift amounts #2477
    * [OptimizationBarrier] give the module a name in generated verilog #2507

  * decode: improve runtime https://github.com/chipsalliance/rocket-chip/pull/2462


  * Switch to using Github Actions:
    * https://github.com/chipsalliance/rocket-chip/pull/2465
    * #2472
    * #2530
    * #2536
  * Some Travis changes were made, but travis is dropped in later releases:
    * #2451
    * #2454
    * #2455
    * #2490
  * Add scalatest to a bucket for regression testing https://github.com/chipsalliance/rocket-chip/pull/2511

  * RTLSim trace log:
    * fixed an issue where the wrong destination register being dumped in the RTLSim trace log https://github.com/chipsalliance/rocket-chip/pull/2409/
    * enhanced log so only registers read or written are printed https://github.com/chipsalliance/rocket-chip/pull/2414

  * add CONTRIBUTING.md https://github.com/chipsalliance/rocket-chip/pull/2342 https://github.com/chipsalliance/rocket-chip/pull/2473

  * [TLBusWrapper] more stability to internal wire names https://github.com/chipsalliance/rocket-chip/pull/2515

  * [LazyRoCC] convert LazyRoCC to chisel3 https://github.com/chipsalliance/rocket-chip/pull/2553

  * [wake]
    * add self-location rules https://github.com/chipsalliance/rocket-chip/pull/2526
    * fix string interpolation of bootrom path https://github.com/chipsalliance/rocket-chip/pull/2535
    * publish location of ivydependencies.json https://github.com/chipsalliance/rocket-chip/pull/2540
    * update CI to 0.19.0 https://github.com/chipsalliance/rocket-chip/pull/2594 (supercedes https://github.com/chipsalliance/rocket-chip/pull/2584)
    * avoid hardcoded directory path for hardfloat repo https://github.com/chipsalliance/rocket-chip/pull/2633

  * [mill] add mill build system https://github.com/chipsalliance/rocket-chip/pull/2654

* TLMonitors: formal verification support and additional constraints
  * TLVIP2: https://github.com/chipsalliance/rocket-chip/pull/2271
    * follow up checking whether packets are diplomatically valid https://github.com/chipsalliance/rocket-chip/pull/2505
      * "`supports*`/`emits*`" and "Fast-or-Safe" naming scheme reintroduced https://github.com/chipsalliance/rocket-chip/pull/2754
    * channel C-D properties https://github.com/chipsalliance/rocket-chip/pull/2537
    * no Diplomacy in error messages https://github.com/chipsalliance/rocket-chip/pull/2573
  * change `isShrink` `TLPermissions` assertion on C channel to `isReport` https://github.com/chipsalliance/rocket-chip/pull/2675

* TLEdge: add require failure messages for TL edges https://github.com/chipsalliance/rocket-chip/pull/2313/
* minor tilelink v1 parameter fixes for setName and probe rendering
  * https://github.com/chipsalliance/rocket-chip/pull/2428
* add v2 constructors to TL Parameters https://github.com/chipsalliance/rocket-chip/pull/2532
* https://github.com/chipsalliance/rocket-chip/pull/2571

* [TLParameters] functions to look at emits parameters https://github.com/chipsalliance/rocket-chip/pull/2572

* APBToTL: only assert address alignment when data is ready and valid on a-channel https://github.com/chipsalliance/rocket-chip/pull/2314

* [BundleBridge] generalize `BundleBroadcast` into `BundleBridgeNexus` https://github.com/chipsalliance/rocket-chip/pull/2497
  * user can now supply input and output functions

* [BundleBridge] add `SafeRegNext` to `BundleBridgeNexus` to preserve width https://github.com/chipsalliance/rocket-chip/pull/2520
* [BundleBroadcast] add register pipelining argument
  * https://github.com/chipsalliance/rocket-chip/pull/2431

* TL user bits
  * drive AMBAProt bits:
    * [TLBroadcast] [TLCacheCork] https://github.com/chipsalliance/rocket-chip/pull/2457
    * [SBA] https://github.com/chipsalliance/rocket-chip/pull/2448
    * [D$][I$][Hella$] allow AMBA prot fields to be carried over TL on conversion https://github.com/chipsalliance/rocket-chip/pull/2383
  * [TLBroadcast][TLSourceShrinker] pass through user bits
    * https://github.com/chipsalliance/rocket-chip/pull/2446


* [TLBroadcast] add API to create Probe filters for Broadcast coherence manager  https://github.com/chipsalliance/rocket-chip/pull/2509
* [TLBroadcast] fixed a Generator bug when instantiated with no inner cache https://github.com/chipsalliance/rocket-chip/pull/2516
* [TLBroadcast] Add control parameters for control interface https://github.com/chipsalliance/rocket-chip/pull/2519

* make it possible to filter with Banked Broadcast Hub https://github.com/chipsalliance/rocket-chip/pull/2545

* [TLSourceShrinker] preserve meta data when no shrinkage is required #2466
* [TLFragmenter] ensure Fragmenter raises corrupt signal when raising denied #2468
* [Tilelink][Arbiter][Xbar][ReadyValidCancel] Add new API that replaces `valid` with `earlyValid` and `lateCancel` to fix a timing path for A-channel requests https://github.com/chipsalliance/rocket-chip/pull/2480 https://github.com/chipsalliance/rocket-chip/pull/2488

* [TLCacheCork] prevent cache block write size from exceeding read size https://github.com/chipsalliance/rocket-chip/pull/2527
* [TLCacheCork] switch CacheCork class to take a case class parameter https://github.com/chipsalliance/rocket-chip/pull/2684
  * with backwards compatible constructor in helper object


* [TLBundle] C channel now has same user bits as A channel https://github.com/chipsalliance/rocket-chip/pull/2632
  * caches now responsible for driving AMBAProt on C-channel.

* [TLArbiter] add `highestIndexFirst` arbitration policy https://github.com/chipsalliance/rocket-chip/pull/2587

* [AHBToTL] retain AHB hrdata even during error response https://github.com/chipsalliance/rocket-chip/pull/2512
* [AHBToTL] fix spurious fire of assertion on first cycle https://github.com/chipsalliance/rocket-chip/pull/2523

* [CreditedIO] introduce new DecoupledIO interface for credit debit buffers https://github.com/chipsalliance/rocket-chip/pull/2555


* [IdMap][IdMapEntry] standardize IdMap and IdMapEntry https://github.com/chipsalliance/rocket-chip/pull/2483
  * [AXI4IdIndexer] later fixed a bug with graphml parsing metadata bracketed in "< >" https://github.com/chipsalliance/rocket-chip/pull/2638

* [IdMapEntry][OMIdMapEntry] add `maxTransactionsInFlight` field https://github.com/chipsalliance/rocket-chip/pull/2627

* [TLRAM] improved cycle time for designs involving TLRAM https://github.com/chipsalliance/rocket-chip/pull/2582

* [SRAM] accomodate address ranges that require more than 32 bits https://github.com/chipsalliance/rocket-chip/pull/2491
* [SimAXIMem] introduce `base` address argument to constructor https://github.com/chipsalliance/rocket-chip/pull/2628
* [SRAM] Add public accessors for SRAM modules https://github.com/chipsalliance/rocket-chip/pull/2646

* [AXI4Deinterleaver][AXI4IdIndexer][AXI4UserYanker][TLToAXI4][Anotations] https://github.com/chipsalliance/rocket-chip/pull/2676
   * Scala doc
   * Clarifying comments
   * Unify `TLToAXI4` metadata code paths into a single path through `TLtoAXI4IdMap`
   * Make any value of `TLToAXI4.stripBits` other than 0 illegal and stop using it internally.
   * Remove usage of un-consumed `Annotated.idMapping` and delete associated application and annotation class.

* [AXI4Deinterleaver] support asynchronous reset  https://github.com/chipsalliance/rocket-chip/pull/2479/
* [AXI4Deinterleaver] add buffer when optimized away https://github.com/chipsalliance/rocket-chip/pull/2642 https://github.com/chipsalliance/rocket-chip/pull/2652

* [AXIS] allow masters to carry resources #2443

* [BasicBusBlocker] convert to chisel3, add scala-doc, add factory companion object https://github.com/chipsalliance/rocket-chip/pull/2630

* [PhysicalFilter] added scaladoc and `RegFieldDesc` #2685

Version 1.3

This version exists as a branch, but seems to be largely synonymous with 1.2. There is no release for this version.

Version 1.2

There are no existing release notes for these versions.