# ladspa applyplugin scripts

## # calf compressor

### applyseplugin

```
analyseplugin calf.so|grep -i compress -A20
```

output

```
Ports:	"In L" input, audio
	"In R" input, audio
	"Out L" output, audio
	"Out R" output, audio
	"Bypass" input, control, toggled, default 0
	"Input" input, control, 0 to 64, default 1
	"Output" input, control, 0 to 64, default 1
	"Input L" output, control, 0 to 1, default 0
	"Input R" output, control, 0 to 1, default 0
	"Output L" output, control, 0 to 1, default 0
	"Output R" output, control, 0 to 1, default 0
	"0dB-InL" output, control, 0 to 1, default 0
```

### applyplugin without param
```
applyplugin \
$1 \
$1 \
calf.so \
Compressor
```
output

```
Plugin "Calf Compressor LADSPA" has the following control inputs:
	Bypass
	Input (0 to 64)
	Threshold (0.000976563 to 1)
	Ratio (1 to 20)
	Attack (0.01 to 2000)
	Release (0.01 to 2000)
	Makeup Gain (1 to 64)
	Knee (1 to 8)
	Detection (0 to 1)
	Stereo Link (0 to 1)
```

### using applyplugin

```
if [ -z $1 ];then
echo "usage arg1=src/my.wav"
else

se1=$(echo $1|sed s/src\\///g)

# comp

applyplugin \
$1 \
$1.wav \
calf.so \
Compressor \
0 \
10 \
0.25 \
10 \
4.4 \
200 \
5 \
2.75 \
1 \
0


fi

```

## # dyson comp
### analyseplugin

```
analyseplugin dyson_compress_1403.so|grep -i compress -A20
```
output

```
Ports:	"Peak limit (dB)" input, control, -30 to 0, default 0
	"Release time (s)" input, control, 0 to 1, default 0.25
	"Fast compression ratio" input, control, 0 to 1, default 0.5
	"Compression ratio" input, control, 0 to 1, default 0.5
	"Input" input, audio
	"Output" output, audio
```

### applyplugin without param
```
if [ -z $1 ];then
echo "usage arg1=wav"
else

applyplugin \
$1 \
$1 \
dyson_compress_1403.so \
dysonCompress

fi
```
### using applyplugin

```
if [ -z $1 ];then
echo "usage arg1=src/my.wav"
else

se1=$(echo $1|sed s/src\\///g)

# comp

applyplugin \
rat/$se1 \
dys/$se1 \
dyson_compress_1403.so \
dysonCompress \
0 \
0.25 \
.5 \
.5


fi
```

## # caps comp

```
applyplugin \
$se1 \
$se1 \
caps.so \
Compress \
5 \
5 \
.5 \
.5 \
100 \
1
```

## # vlevel comp

```
applyplugin \
str/$se1 \
vle/$se1 \
vlevel-ladspa.so \
vlevel_stereo \
2.5 \
0.75 \
1 \
10 \
1
```
