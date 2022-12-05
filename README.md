#!/bin/bash

#Alles über Backups
# Autor:Michael Rößler
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
	echo "| Wo soll das Backup gespeichert werden:    |"
	echo "|                                              |"
	read -p "| Eingabe: " WHERE2BACKUP
}


function what2Backup(){
	clear
	echo "|----------------------------------------------|"
	echo "| Was soll als Backup gespeichert werden:    |"
	echo "|                                              |"
	read -p "| Eingabe: " WHAT2BACKUP
}
