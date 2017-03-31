# ladspa applyplugin scripts

## calf compressor

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

## using applyplugin 
### 
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
