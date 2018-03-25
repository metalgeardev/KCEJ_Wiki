# Game Command Language

## Description
Game Command Language (GCL) is a scripting language developed by KCE Japan West for Metal Gear Solid. GCL is compiled to bytecode and relies on an interpreter library (LibGCL) in the system program. Tcl was used for reference when designing the language.

## Syntax examples
Identifiers written in Japanese are accepted. Comments are handled the same as in C/C++, as well as with the # character for a single-line comment.

### Metal Gear Solid 2: Sons of Liberty
```
chara ドア DoorA1 \
	-kms std_door \
	-position 9325,0,-5050 \
	-rotate 0,2048,0

trap DoorA1_Area スネーク \
	-mask 入る \
	-exec {
		mesg ドア DoorA1 open
	}
```
### Metal Gear Solid 4: Guns of the Patriots
```
/******************************************************************************************/
proc ライト設定 {
	#if d:vardef::DEBUG_PRINT
		print '*** Light setting *** @ライト設定';
	#endif

	command フォグ設定 \
//		-near	-5000			\	//command フォグ設定
//		-far	170000			\	//command フォグ設定
//		-light	0 337			\	//command フォグ設定
//		-rgb	188 635 811		\	//command フォグ設定
//		-before_near 1000 \
//		-before_far 100000 \
//		-before_rbg 1000 1000 784 \
//		-before_limit 1 500
		-rgb 290 376 313	\	//command フォグ設定
		-near -15000		\	//command フォグ設定
		-far 324700			\	//command フォグ設定
		-limit 0 392			//command フォグ設定

	command ライト設定 \
//		-dir				-1016 -2377 -4279	\	// command ライト設定
//		-color				1388 372 0		\	// command ライト設定
//		-chara_color			2870 372 0		\	// command ライト設定
//		-hemispherelight_dir		609 -4921 641		\	// command ライト設定
//		-hemispherelight_frontcolor	149 227 188 784		\	// command ライト設定
//		-hemispherelight_backcolor	15 74 94 784			// command ライト設定
		-dir -1668 -2356 -4082					\	// command ライト設定
		-color 1803 1803 1803					\	// command ライト設定
		-chara_color 815 815 815				\	// command ライト設定
		-hemispherelight_dir 609 -4921 641			\	// command ライト設定
		-hemispherelight_frontcolor 86 86 86 1372	\	// command ライト設定
		-hemispherelight_backcolor 62 62 62 1176			// command ライト設定
}


/******************************************************************************************/
//	Proc name	: エフェクト設定
//	In value	:
//				:
//	Out value	:
//
/******************************************************************************************/
//	How to USE	:
//				:
/******************************************************************************************/
```

Note: This example may contain errors as it was copied by hand from a slightly blurry screen. ([Image 1](mgs4_excerpt1a.png)) ([Image 2](mgs4_excerpt1b.png))

```
// ステージ内のオブジェクトやエフェクトの設定や条件による
// 設定の変更をするサンプル
 
// ステージの設置
chara ステージ設置 ステージモデル \
	-pos 0,0,0 -model d:ステージモデル名
 
// 細かいオブジェクトの設置するプロシージャを呼び出す
@ステージオブジェクト設置処理
 
// エフェクトの起動するプロシージャを呼び出す
if ( $i:時間帯 == d:時間帯:朝 ){
	@ステージエフェクト_朝_起動処理
} else if ( $i:朝昼夜 == d:時間帯:昼 ){
	@ステージエフェクト_昼_起動処理
} else {
	@ステージエフェクト_夜_起動処理
}
```
```
// プレイヤーキャラの定義
chara プレイヤー[NewPlayer] $s:名前 \
	-model $s:モデル名<model> \
	-motion $s:モーション名<motion> \
	…
```

## Compilation
An in-house tool was developed for compiling GCL scripts. The tool for MGS1 was named "GCLCONV" and was written by lead programmer Kazunobu Uehara.

The compiled files will be named "__scenerio.gcx__" and sorted into the proper stage. There can also be additional GCX files in a given stage. In MGS1, the demo theater sequence loads "__demo.gcx__", and MGS2's boss rush mode loads "__boss.gcx__".

__RADIO.DAT__ in MGS1 and __CODEC.DAT__ in following games contain GCX scripts concatenated into a streaming-type DAT archive.

The "scenerio" misspelling has persisted from MGS1 into MGS3D. Konami has since dropped GCL in favor of Lua scripting for the Fox Engine.

### Zone of the Enders
The equivalent compiled files in ZOE and ZOE2 have the extension "__SCX__" and are named after the stage they control. For example: __stage/gl1/gl1.scx__

The interpreter library is named LibSCN.


## GCX format description

### Timestamp
The first four bytes of each GCX script (excluding MGS1) are a Unix hexadecimal timestamp in little endian format. All scripts for a given build of a game in both __stage__ and __codec__ share the same timestamp.

Convert it to big endian and input it into a [conversion tool](https://www.epochconverter.com/hex) to see when the scripts were compiled.

### Date Table

| Hex Value (LE) | Title | Product Code/Notes | Time (GMT) |
| ----- | ----- | ----- | ----- |
| ACC4133A | MGS2 Trial Edition | SLPM-62043 | November 16, 2000 11:27:40 AM |
| E18D343A | MGS2 Trial Edition | SLUS-29003 | December 11, 2000 8:18:41 AM |
| E18D343A | MGS2 Trial Edition | SLED-50117 | December 11, 2000 8:18:41 AM |
| 7191B23B | MGS2 Sons of Liberty | SLUS-20144 | September 27, 2001 2:39:45 AM |
| 33F8C43B | MGS2 Sons of Liberty | SLPM-65078 | October 11, 2001 1:38:59 AM |
| ? | MGS2 Sons of Liberty | EU, English/French/German |  |
| ? | MGS2 Sons of Liberty | EU, Italian |  |
| ? | MGS2 Sons of Liberty | EU, Spanish |  |
| ? | MGS2 Sons of Liberty | SLPM-67515, Korean |  |
| 0281273D | Document of MGS2 | SLPM-65184, DOCUMENT | July 6, 2002 11:45:06 PM |
| 33B3293D | Document of MGS2 | SLUS-20543, DOCUMENT | July 8, 2002 3:43:47 PM |
| F1DE323D | Document of MGS2 | SLES-82010, DOCUMENT | July 15, 2002 2:40:49 PM |
| AAB5123D | Document of MGS2 | SLPM-65184, MGS2 | June 21, 2002 5:12:10 AM |
| AAB5123D | Document of MGS2 | SLUS-20543, MGS2 | June 21, 2002 5:12:10 AM |
| AAB5123D | Document of MGS2 | SLES-82010, MGS2 | June 21, 2002 5:12:10 AM |
| FE7A2E3D | MGS2 Substance | US	Xbox, KN007	1.06 | July 12, 2002 6:45:18 AM |
| B92A903D | MGS2 Substance | EU	Xbox, KN007	1.08 | September 24, 2002 9:04:57 AM |
| B92A903D | MGS2 Substance | EU	Win | September 24, 2002 9:04:57 AM |
| B92A903D | MGS2 Substance | US	Win | September 24, 2002 9:04:57 AM |
| 3D88923D | MGS2 Substance | SLUS-20554 | September 26, 2002 4:08:29 AM |
| ? | MGS2 Substance | SLPM-67002 | |
| ? | MGS2 Substance | SLES-82009 | |
| ? | MGS2 Substance | SLKA-35001 | |
| D7B8E13F | MGS The Twin Snakes | US Debug v099.1 | December 18, 2003 2:25:27 PM |
| C35C1C40 | MGS The Twin Snakes | DOL-P-GGSE | February 1, 2004 1:56:19 AM |
| 44AA2140 | MGS The Twin Snakes | DOL-P-GGSJ | February 5, 2004 2:28:20 AM |
| D9912240 | MGS The Twin Snakes | DOL-P-GGSP | February 5, 2004 6:56:25 PM |
| 85A0DA40 | MGS3 Trial Edition | SCUS-97339 | June 24, 2004 9:36:05 AM |
| DC156341 | MGS3 Snake Eater | SLPM-65790 | October 5, 2004 9:45:00 PM |
| BEBA6541 | MGS3 Snake Eater | SLUS-20915 | October 7, 2004 9:53:02 PM |
| ? | MGS3 Snake Eater | EU, English/French | |
| ? | MGS3 Snake Eater | EU, German | |
| ? | MGS3 Snake Eater | EU, Italian | |
| ? | MGS3 Snake Eater | EU, Spanish | |
| ? | MGS3 Snake Eater | SLKA-25251 | |
| 32DC9941 | MG AC!D | ULJM-05001 | November 16, 2004 10:53:38 AM |
| D268EC41 | MG AC!D | ULUS-10006 | January 18, 2005 1:39:30 AM |
| D268EC41 | MG AC!D | ULES-00008 | January 18, 2005 1:39:30 AM |
| 5FFE4243 | MG AC!D 2 | ULJM-05047 | October 4, 2005 10:12:47 PM |
| 8EEB8F43 | MG AC!D 2 | ULUS-10077 | December 2, 2005 6:37:02 AM |
| 8EEB8F43 | MG AC!D 2 | ULKS-46065 | December 2, 2005 6:37:02 AM |
| 8EEB8F43 | MG AC!D 2 | ULES-00284 | December 2, 2005 6:37:02 AM |
| D3743843 | MGS3 Subsistence | SLPM-66220~2 | September 26, 2005 10:23:15 PM |
| DBBE7143 | MGS3 Subsistence | SLUS-21359 (+2) | November 9, 2005 9:18:19 AM |
| 20DC8643 | MGS3 Subsistence | SLKA-25353~5 | November 25, 2005 9:40:48 AM |
| 05D3D543 | MGS3 Subsistence | EU, Italian | January 24, 2006 7:11:01 AM |
| A3F7DF43 | MGS3 Subsistence | EU, German | January 31, 2006 11:49:55 PM |
| 0FD3E643 | MGS3 Subsistence | EU, English/French | February 6, 2006 4:39:43 AM |
| 79DDE643 | MGS3 Subsistence | EU, Spanish | February 6, 2006 5:24:09 AM |
| FB57F143 | MGS3S Online Beta Test | TLES-82043 | February 14, 2006 4:09:31 AM |
| ? | Marugoto Metal Gear Online | SLPM-68524 | |
| ? | Metal Gear & Metal Gear 2 | SLPM-66795 | |
| 9CE13145 | MPO | ULJM-05193 | October 15, 2006 7:22:04 AM |
| 9CE13145 | MPO | ULUS-10202 | October 15, 2006 7:22:04 AM |
| CD455D45 | MPO | ULES-00645 | November 17, 2006 5:17:01 AM |
| D6498A46 | MPO+ | ULJM-05261 | July 3, 2007 1:06:30 PM |
| D6498A46 | MPO+ | ULUS-10290 | July 3, 2007 1:06:30 PM |
| D6498A46 | MPO+ | ULES-01003 | July 3, 2007 1:06:30 PM |
| ? | MGS4 Guns of the Patriots | BLJM-67001 | |
| 5E1AE247 | MGS4 Guns of the Patriots | BLUS-30109 | March 20, 2008 8:03:42 AM |
| 5E1AE247 | MGS4 Guns of the Patriots | BLES-00246 | March 20, 2008 8:03:42 AM |
| 5E1AE247 | MGS4 v2.00 | BLES-00246 v2.00 patch | March 20, 2008 8:03:42 AM |
| 56ECBC47 | MGO2 Premier Beta | NPJB-90090 | February 21, 2008 3:13:26 AM
| 591AD947 | MGO2 Premier Beta | NPJB-90090 | March 13, 2008 12:13:13 PM
| ? | MGO2 Premier Beta | NPUB-90086 | |
| ? | MGO2 Premier Beta | BLET-70000 | |
| BC953449 | MGO2 Demo | NPEB-90122 | December 2, 2008 1:56:12 AM
| ? | MGO2 | too many updates | ??? |
| E1F43B48 | MGS4 Database | NPUB-90126 or NPEB-00027 | May 27, 2008 11:47:45 AM |
| 638EDB48 | MGS4 Demo Version | NPUB-90176 | September 25, 2008 1:13:07 PM |
| 5DB1EA48 | MGS4 Demo Version | NPJB-90149 | October 7, 2008 12:46:21 AM |
| ? | MGS4 Demo Version | NPEB-90116 | |
| ? | MGS Peace Walker Demo Ops | NPJH-90063 | |
| ? | MGS Peace Walker Demo Ops | NPUH-90066 | |
| ? | MGS Peace Walker Demo Ops | NPEH-90023 | |
| 063B5D4B | MGS Peace Walker | NPJH-50045 | January 25, 2010 6:32:38 AM |
| 063B5D4B | MGS Peace Walker | ULUS-10509 | January 25, 2010 6:32:38 AM |
| ? | MGS Peace Walker | ULES-01372 |  |
| FD42764C | Metal Gear Arcade | I36-2011012100 | August 26, 2010 10:33:33 AM |
| B5447C4C | Metal Gear Arcade | I36-2011092900 | August 30, 2010 11:54:29 PM |
| ? | MGS Peace Walker HD Edition | NPJB-00123 (etc) | |
| ? | MGS Peace Walker HD Edition | BLUS-30847 (etc) | |
| ? | MGS Peace Walker HD Edition | NPEB-00686 (etc) | |
| ED73E34E | MGS Snake Eater 3D | CTR-P-AMGJ | December 10, 2011 2:59:57 PM |
| 546DE74E | MGS Snake Eater 3D | CTR-P-AMGE | December 13, 2011 3:20:52 PM |
| 366EE74E | MGS Snake Eater 3D | CTR-P-AMGP | December 13, 2011 3:24:38 PM |
| 3100EA4E | MGS Snake Eater 3D Demo | CTR-T-AMGJ | December 15, 2011 2:12:01 PM |
| EF07EA4E | MGS Snake Eater 3D Demo | CTR-T-AMGP | December 15, 2011 2:45:03 PM |
| 820FEA4E | MGS Snake Eater 3D Demo | CTR-T-AMGE | December 15, 2011 3:17:22 PM |