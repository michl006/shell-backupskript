#!/bin/bash

# Backupscript
# Autor: Michael Rößler
# E-Mail : roesslermi@mail-elektronikschule.de
# Version: 1


function menu(){
	clear
	echo "|---------------------------------------------------|"
	echo "| Haupmenu:                                         |"
	echo "|                                                   |"
        echo "|      Backup erstellen:              B             |"
	echo "|      Inhalt eines Backups:          L             |"
	echo "|      Backup zurück spielen:         R             |"
	echo "|      Backup löschen:                D             |"
	echo "|      Programm beenden:              X             |"
	echo "|                                                   |"
	read -p "| Eingabe: " EINGABE
}


function compress(){
	clear
	echo "|-------------------------------------------|"
	echo "| Kompressionsmethode:                      |"
	echo "|                                           |"
	echo "|      ZIP:                   z             |"
	echo "|      BZIP2:                 j             |"
	echo "|      XZ:                    J             |"
	echo "|                                           |"
	read -p "| Eingabe: " COMPRESS
}


function where2Backup(){
	clear
	echo "|----------------------------------------------|"
	echo "| Wo soll das Backup gespeichert werden:       |"
	echo "|                                              |"
	read -p "| Eingabe: " WHERE2BACKUP
}


function what2Backup(){
	clear
	echo "|----------------------------------------------|"
	echo "| Was soll als Backup gespeichert werden:      |"
	echo "|                                              |"
	read -p "| Eingabe: " WHAT2BACKUP
}
 function where(){
	clear
	echo "|----------------------------------------------------|"
	echo "| Wo soll nach dem Backup gesucht werden:            |"
	echo "|                                                    |"
	read -p "| Eingabe: " WHERE
}
function type(){
	clear
	echo "|----------------------------------------------|"
	echo "| Welcher Datentyp hat das Backup:             |"
	echo "|                                              |"
	read -p "| Eingabe: " TYPE
}

function backup(){
        BACKUPFILE=$(date +%Y%m%d-%H%M%S)-backup.tgz
        YESNO=0
        until [ $YESNO = 1 ]
        do
            compress
            echo "Sind sie sicher, dass sie die option ${COMPRESS} ausführen wollen?"
            read -p "0:nein |1:ja    :" YESNO
        done

        YESNO=0
        until [ $YESNO = 1 ]
        do
            where2Backup
            echo "Sind sie sicher, dass sie hier hin speichern möchten: ${WHERE2BACKUP}?"
            read -p "0:nein |1:ja    :" YESNO
        done

        YESNO=0
        until [ $YESNO = 1 ]
        do
            what2Backup
            echo "Sind sie sicher, dass sie dieses Verzeichnis speichern wollen ${WHAT2BACKUP}?"
            read -p "0:nein |1:ja    :" YESNO
        done


        echo "tar cf - ${COMPRESS} ${WHERE2BACKUP} ${WHAT2BACKUP}"
        sleep 5
}

function unbackup(){
	echo "UNBACKUP"
}

function listbackup(){
	echo "LISTBACKUP"
}

function deletebackup(){
	
        YESNO=0
        until [ $YESNO = 1 ]
        do
            where
            echo "Sind sie sicher, dass sie hier $WHERE nach dem Backup suchen wollen?"
            read -p "0:nein |1:ja    :" YESNO
        done

        YESNO=0
        until [ $YESNO = 1 ]
        do
            type
            echo "Sind sie sicher, dass sie das Backup mit dem Datentyp $TYPE suchen wollen?"
            read -p "0:nein |1:ja    :" YESNO
        done
        
        echo "find $WHERE -name *.$TYPE -typ -f"
        sleep 5
	
	YESNO=0
        until [ $YESNO = 1 ]
        do
            deletebackup
            echo "Sind sie sicher, dass sie das Backup $DELETEBACKUP löschen wollen?"
            read -p "0:nein |1:ja    :" YESNO
        done

	
}

while :
do
	menu
	case $EINGABE in
		b|B)
			backup
			;;
		r|R)
			unbackup
			;;
		l|L)
			listbackup
			;;
		d|D)
			deletebackup
			;;
		*)
			echo "Und Tschüss"
			exit 1
	esac
	sleep 2
done

exit 0

