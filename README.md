# Universal Modbus TCP Client Pro (80 Ch)
**Autor:** Tomasz Gąsiorowski ([@tomikoni](https://github.com/tomikoni))  
**Email:** tomasz.kowalski00@hotmail.com  
**Wersja:** 1.3.3.0  

## Opis
Uniwersalny klient Modbus TCP dla systemu Q-SYS, umożliwiający komunikację z zewnętrznymi urządzeniami (PLC, bramki I/O, falowniki). Wtyczka została napisana w czystym Lua (Pure Lua), co eliminuje problemy z ładowaniem plików XML w nowszych wersjach Q-SYS.

Moduł oferuje **80 niezależnych kanałów** dla każdego typu danych Modbus oraz specjalną funkcję obsługi rejestrów bitowych.

## Funkcje
*   **Coils (0x01/0x05)**: 80 kanałów (Odczyt/Zapis)
*   **Discrete Inputs (0x02)**: 80 kanałów (Tylko odczyt)
*   **Holding Registers (0x03/0x06)**: 80 kanałów (Odczyt/Zapis, 16-bit Integer)
*   **Input Registers (0x04)**: 80 kanałów (Tylko odczyt, 16-bit Integer)
*   **Packed Coils**: 80 kanałów rejestrowych z rozbiciem na bity (16 przycisków na kanał).

## Instalacja
1.  Skopiuj plik `ModbusClientLua80.qplug` do folderu wtyczek Q-SYS:
    *   Zazwyczaj: `Dokumenty > QSC > Q-Sys Designer > Plugins`
2.  Uruchom Q-SYS Designer.
3.  Wtyczka pojawi się w bibliotece w sekcji `User`.

## Konfiguracja (Zakładka "Setup")
*   **Server Address**: Adres IP urządzenia Modbus (np. 192.168.1.10).
*   **Server Port**: Port TCP (domyślnie 502).
*   **Bus Address**: Adres urządzenia na magistrali (Unit ID), zazwyczaj 1.
*   **Polling Time**: Czas w milisekundach między odpytaniami (np. 1000ms).
*   **Timeout**: Maksymalny czas oczekiwania na odpowiedź.

## Obsługa Kanałów
Każdy kanał posiada następujące kontrolki:
*   **En (Enable)**: Włącza/wyłącza odpytywanie danego kanału.
*   **Addr**: Adres rejestru Modbus (0-65535).
*   **Val**: Aktualna wartość odczytana z urządzenia.
*   **Ovr (Override)**: Wymuszenie wartości wyjściowej (pomija odczyt z pinu wejściowego).
*   **Sync**: (Tylko wyjścia) Aktualizuje wartość w Q-SYS, jeśli zostanie zmieniona przez inne urządzenie.

## Nowość: Zakładka "Packed Coils"
Ta funkcja pozwala na sterowanie rejestrami 16-bitowymi za pomocą pojedynczych bitów. Jest to idealne do sterowania maszynami, które mapują stany (np. Start, Stop, Reset) na poszczególne bity jednego rejestru.

*   **Ilość**: 80 Rejestrów.
*   **Sterowanie**: Każdy rejestr posiada **16 przycisków** (0-15).
*   **Działanie**:
    *   Kliknięcie przycisku bitu (np. bit 0) zmienia wartość całego rejestru (np. z 0 na 1).
    *   Kliknięcie bitu 1 zmienia wartość na 2 (lub 3, jeśli bit 0 też jest włączony).
    *   Wartość jest natychmiast wysyłana do urządzenia.
    *   Zmiana wartości w urządzeniu automatycznie aktualizuje stan przycisków w wtyczce.

---
*Created by Tomasz Gąsiorowski*
