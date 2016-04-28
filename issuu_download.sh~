#! /bin/bash

#================================================================
# HEADER
#================================================================
#% SYNOPSIS
#+    issuu_download [-i="...."] [-o="..."] [-t="..."] [--pages=...]
#+    ${SCRIPT_NAME} [-hv] [-o[file]] args ...
#%
#% DESCRIPTION
#%    Script para descargar pdfs del sitio https://issuu.com
#%
#% OPTIONS
#%    -o=[folder], --output=[folder]    Directorio donde guardar el pdf
#%    -p=[number], --pages=[number]     Paginas totales del pdf
#%    -i=[UID], --id=[UID]              Identificador del pdf en issuu
#%    -t=[string], --title=[string]     Título del pdf exportado
#%
#% EXAMPLES
#%    issuu_download.sh -i="100713223833-42cebcdb74f8412e83a9811681dd47f2" -o="/tmp/" -t="Física de la escalada" --pages=16
#%
#================================================================
#- IMPLEMENTATION
#-    version         1.0.0
#-    author          Federico Lozada Mosto
#-    copyright       Copyright (c) http://www.mostofreddy.com.ar
#-    license         MIT
#-
#================================================================
#  HISTORY
#     2016/04/24 : mostofreddy : Script creation
# 
#================================================================
# END_OF_HEADER
#================================================================

cat << "EOF"
 ___ ____ ____  _   _ _   _ 
|_ _/ ___/ ___|| | | | | | |
 | |\___ \___ \| | | | | | |
 | | ___) |__) | |_| | |_| |
|___|____/____/ \___/ \___/ 
 ____   _____        ___   _ _     ___    _    ____  
|  _ \ / _ \ \      / / \ | | |   / _ \  / \  |  _ \ 
| | | | | | \ \ /\ / /|  \| | |  | | | |/ _ \ | | | |
| |_| | |_| |\ V  V / | |\  | |__| |_| / ___ \| |_| |
|____/ \___/  \_/\_/  |_| \_|_____\___/_/   \_\____/ 

                                                     
EOF

# Vars
#==============================================================================
START=1
TITLE=
PAGES=
OUTPUT=
ID=

# Functions
#==============================================================================
function ProgressBar {
    # Process data
    let _progress=(${1}*100/${2}*100)/100
    let _done=(${_progress}*4)/10
    let _left=40-$_done
    # Build progressbar string lengths
    _fill=$(printf "%${_done}s")
    _empty=$(printf "%${_left}s")
 
    # 1.2 Build progressbar strings and print the ProgressBar line
    # 1.2.1 Output example:
    # 1.2.1.1 Progress : [########################################] 100%
    printf "\rDownload images : [${_fill// /#}${_empty// /-}] ${_progress}%%"
}

# Get command line params
#==============================================================================
for i in "$@"
do
case $i in
    -p=*|--pages=*)
    PAGES="${i#*=}"
    ;;
    -i=*|--id=*)
    ID="${i#*=}"
    ;;
    -o=*|--output=*)
    OUTPUT="${i#*=}"
    OUTPUT=`echo ${OUTPUT} | sed 's/ /_/g;'`
    OUTPUT=`echo "${OUTPUT}" | sed s,/,\\\\\\\\\\/,g`
    ;;
    -t=*|--title=*)
    TITLE="${i#*=}"
    TITLE=`echo ${TITLE} | sed 's/ /_/g;'`
    ;;
    *)
            # unknown option
    ;;
esac
done

# If any var is empty 
#==============================================================================
if [[ -z $TITLE ]]; then
	printf "Title: " ; read -r TITLE
	TITLE=`echo ${TITLE} | sed 's/ /_/g;'`
fi

if [[ -z $OUTPUT ]]; then
	printf "Output folder: " ; read -r OUTPUT
	OUTPUT=`echo ${OUTPUT} | sed 's/ /_/g;'`
	OUTPUT=`echo "${OUTPUT}" | sed s,/,\\\\\\\\\\/,g`
fi

if [[ -z $ID ]]; then
	printf "Document ID: " ; read -r ID
fi

if [[ -z $PAGES ]]; then
	printf "Total pages: " ; read -r PAGES
fi

# Script 
#==============================================================================

OUTPUT=$OUTPUT"\/"$TITLE

# download images
for (( c=1; c<=$PAGES; c++ ))
do
	sleep 0.1
    	ProgressBar ${c} ${PAGES}
	wget -q -O "images/page_$c.jpg" "https://image.issuu.com/$ID/jpg/page_$c.jpg" > /dev/null
done
echo 

echo "Please wait... creating file"
ls images/page_*.jpg | sort -n -t _ -k 2 | tr '\n' ' ' | sed "s/$/\ ${OUTPUT}.pdf/" | xargs convert  -quality 100 -quality 100 

echo 
echo "file saved in: "$OUTPUT

# remove images
rm images/*
echo 
