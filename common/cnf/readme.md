# Data Configuration Files

## Description
Data configuration files (data.cnf) are used by derivatives of the MGS engine to determine what files to load in a given data set of non-streamed data (__stage__, __face__, __slot__). Although always present when the files are left unpackaged, data.cnf files are excluded when the DIR/DAT archives are built as the relevant information is included in the binary header.

## Syntax & Examples
Lines beginning with a single period (".resident", for example) are used to set flags regarding into which portion of memory the following files are to be loaded.

### Metal Gear Solid: Integral (Windows)
Sample: [stage.mgz/stage/init/data.cnf](sample/mgs_pc/init.cnf)

Sample: [stage.mgz/stage/s00a/data.cnf](sample/mgs_pc/s00a.cnf)

Sample: [stage.mgz/stage/s01a/data.cnf](sample/mgs_pc/s01a.cnf)

| flag | data |
| ----- | ----- |
| .resident | res_mdl1.dar / .res |
| .nocache | .bin / .dar (textures) |
| .sound | .mdx / .efx / .wvx |
| .cache | all other data |

Note: Most data.cnf files in this port have timestamps that date before the release of Integral for the PlayStation. They're likely unmodified from KCE Japan's originals as the PC port started development nearly one year after Integral had been released.

### Metal Gear Solid 2: Substance (Windows)
Sample: [cdrom.img/face/f00a/data.cnf](sample/mgs2_pc/f00a.cnf)

Sample: [cdrom.img/stage/r_tnk0/data.cnf](sample/mgs2_pc/r_tnk0.cnf)

Sample: [cdrom.img/stage/w00a/data.cnf](sample/mgs2_pc/w00a.cnf)

| flag | data |
| ----- | ----- |
| .face | face.dar / face.qar |
| .nocace | .bin |
| .resident | resident.dar / resident.qar |
| .cache | all other data |

Note: Texture archives (.qar files) are prefixed with "@".

Note: Unlike MGS1, the sound packages (.sdx) are not listed.

### Metal Gear Solid: The Twin Snakes
Sample: [shared/stage/preview/data.cnf](sample/mgstts/preview.cnf)

| flag | data |
| ----- | ----- |
| .nocache | _none_ (the game does not use overlays) |
| .cache | all other data |

The Twin Snakes uses a stage.dat archive. This is the only file remaining in the __shared/stage__ directory on the disc (US & JP versions). This file is not present on either disc for debug build v099.1 or the EU release. It's highly likely the rest followed the same rules as MGS2.

### Metal Gear Solid: Portable Ops & Peace Walker
Sample: [USRDIR/stage/r_main01/_zar/data.cnf](sample/mpo/r_main01.cnf) (MPO)

Sample: [USRDIR/stage/st01/_zar/data.cnf](sample/mpo/st01.cnf) (MPO)

Sample: [USRDIR/STAGEDAT.PDT/r_main01/data.cnf](sample/mgspw/r_main01.cnf) (MGSPW)

Sample: [USRDIR/STAGEDAT.PDT/w00s01a/w00s01a.cnf](sample/mgspw/w00s01a.cnf) (MGSPW)

| flag | data |
| ----- | ----- |
| .nocache | _none_ |
| .resident | resident.dar / resident.qar / resident.vfp |
| .slot | _references to slot files_ |
| .endslot | _ends the slot reference_ |
| .cache | all other data |

Metal Gear AC!D, operates in the same way, albeit without the slot system from MGS3.

### Metal Gear Solid 4: Guns of the Patriots
Sample: [USRDIR/mgs/stage/init/data.cnf](sample/mgs4/init.cnf)

Sample: [USRDIR/mgs/stage/mg_setup/data.cnf](sample/mgs4/mg_setup.cnf)

Sample: [USRDIR/mgs/stage/mg_setup1/data.cnf](sample/mgs4/mg_setup1.cnf)

Sample: [USRDIR/mgs/stage/title/data.cnf](sample/mgs4/title.cnf)

Sample: [USRDIR/mgs/stage/r_sna01/data.cnf](sample/mgs4/r_sna01.cnf) (MGS4 Demo Version)

Sample: [USRDIR/mgs/stage/s01a10l/data.cnf](sample/mgs4/s01a10l.cnf) (MGS4 Demo Version)

| flag | data |
| ----- | ----- |
| .nocache | _none_ |
| .resident | resident.dar / resident.qar / resident.vfp |
| .slot | _references to slot files_ |
| .endslot | _ends the slot reference_ |
| .cache | all other data |
| .delayload | *_d.dlz |
| .delayload_w | .dlz  / *_nodld.dlz |

Note: The same flags tend to appear multiple times.

### Metal Gear Solid: Snake Eater 3D
Sample: [romFS/stage/r_sna01/data.cnf](sample/mgs3d/r_sna01/data.cnf)

Sample: [romFS/stage/s000a_0/data.cnf](sample/mgs3d/s000a_0/data.cnf)

| flag | data |
| ----- | ----- |
| .nocache | _none_ (the game does not use overlays) |
| .resident | resident.hpk|
| .slot | _references to slot files_ |
| .endslot | _ends the slot reference_ |
| .cache | cache.hpk / scenerio.gcx |

### Anubis: Zone of the Enders HD Edition

Sample: [ZoE2/stage/init/data.cnf](sample/zoe2hd/init/data.cnf)

Sample: [ZoE2/stage/vr01/data.cnf](sample/zoe2hd/vr01/data.cnf)

Sample: [ZoE2/stage/zakat/data.cnf](sample/zoe2hd/zakat/data.cnf)

| flag | data |
| ----- | ----- |
| _none_ | .bin |
| .cache | local.fnt / .scx |

These are likely carried over (and possibly modified) from the original PS2 source assets, as ZOE2 HD used a STAGE.DAT archive equivalent to the original release.