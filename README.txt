NX9-linuxcnc-lathe-PP
=====================

Postprocessor for using a 2-axis LinuxCNC lathe in NX9 CAM

experimental.

Beachten: die ausgegebenen Koordinaten beziehen sich in NX und LinuxCNC immer auf den Kontrollpunkt des Werkzeugs, der in Verlängerung der WSP-Spitze liegt: http://www.linuxcnc.org/docs/html/lathe/lathe-user.html#_control_point

Wichtige eingebaute Workarounds/Änderungen:
Auto Wkz.Wechsel und manuellen Wkz. wechsel angleichen
H00/01 weg (Angabe des Werkzeughalters)
Workaround mit custom Tcl file, um MOM_first_turret warning wegzubekommen
besondere Zeilennummerierung ":" statt "N" bei Wkz.Wechsel weg
F nach G95 stets angeben -> Workaround: wird bei linear move stets angegeben
FROM-Move wird zwangsweise am Anfang einer Op. ausgeführt (zuerst in Z und dann in X), weil sonst vom Endpunkt einer Operation im Eilgang quer durchs Werkstück zum nächsten Startpunkt verfahren wurde. Für Innendrehen muss unbedingt ein TO-Move nach der Drehbewegung konfiguriert werden.

TODO:
Delay Revolutions ist zur Zeit auf Delay seconds umgebogen
G7/G8 Durchm/Radius Modus erzwingen

WONTFIX:
Wkz.nummer 0 sagt "bitte Wkz entnehmen"
Gewinde mit variabler Steigung (thread increment) werden nicht unterstützt, weil LinuxCNC das nicht kann.
Max. RPM bei konst. Schnittgeschwindigkeit muss angegeben werden, sonst stoppt der PP mit Fehler. (LinuxCNC würde sonst evtl stehenbleiben)
diverse ungenutzte Codes wurden auf G50 (=gibts nicht) gesetzt. (Wenn doch einer auftaucht, muss man mit dem Review Tool suchen wo der herkommt und das dem PP beibringen)