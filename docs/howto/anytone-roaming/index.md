# Anytone DMR Roaming Guide

This guide explains how to set up and use DMR roaming with Anytone radios, focusing on the Anytone 890 handheld with compatibility notes for the 578 mobile and 168 handheld models. The provided files cover Michigan-area repeaters for automatic roaming operation.

## What is DMR Roaming?

DMR roaming allows your radio to automatically select the strongest repeater from a predefined group when you're traveling or in areas with multiple repeaters. Instead of manually switching channels, the radio scans for the best signal and connects you automatically.

Note about Anytone vs Motorola:

Anytone roaming behaves differently than roaming on many Motorola radios. While Anytone radios do support automatic roaming, in practice the most reliable workflow is to perform a manual, one‑time roam on demand (select a zone, then use One Time Roaming). This documentation focuses on that on‑radio, one‑time roam workflow and shows how to program the files into CPS for that use case.

Repeater ownership and etiquette:

The repeaters included in these CSV files are CMEN repeaters located in Michigan. Before using any CMEN repeater, please review CMEN's rules and etiquette at https://w8cmn.net/dmr/. CMEN is not affiliated with the Who Cares Amateur Radio Group; this guide is provided as a primer only.

**Benefits:**
- **Automatic Operation**: No manual channel switching while traveling
- **Optimal Signal**: Always connected to the strongest repeater
- **Seamless Communication**: Maintain contact across wide geographic areas
- **Michigan Coverage**: Covers major population centers across the state

## Understanding the Roaming Files

This guide includes two CSV files that work together:

- **[RoamingZone.CSV](RoamingZone.CSV)**: Defines 8 geographic roaming zones and their member repeaters
- **[RoamingChannel.CSV](RoamingChannel.CSV)**: Contains 35 DMR repeaters with complete technical details

### Download the Roaming Files

You can download the CSVs directly or grab a ZIP bundle containing both files. Click the links below (or right-click → Save As):

- [RoamingChannel.CSV](RoamingChannel.CSV) — Repeater details (35 repeaters)
- [RoamingZone.CSV](RoamingZone.CSV) — Zone definitions (8 zones)
- [anytone-roaming-csvs.zip](anytone-roaming-csvs.zip) — ZIP bundle containing both CSVs

File verification:
- RoamingZone.CSV: ~10 lines, 8 zones covering Michigan areas
- RoamingChannel.CSV: ~37 lines, 35 repeaters with technical specs

## Prerequisites

### Required Software
- **Anytone CPS (Customer Programming Software)**
  - Anytone 890: CPS version 1.03 or later
  - Anytone 578: CPS version 1.13 or later  
  - Anytone 168: CPS version compatible with model
  - Download from [Anytone official site](https://www.anytone.net/download)

### Hardware Requirements
- Anytone 890 handheld (primary focus)
- Anytone 578 mobile or 168 handheld (compatible models)
- USB programming cable (included with radio)
- Computer with Windows (recommended) or Mac/Linux compatibility layer

### CPS Software Installation

1. **Download CPS:** Visit the Anytone website and download the appropriate CPS version for your radio model
2. **Install Drivers:** Install USB programming cable drivers if prompted
3. **Connect Radio:** Plug the programming cable into your computer and radio
4. **Test Connection:** Open CPS and ensure it can read from your radio

## CPS Programming Step-by-Step

### Step 1: Read Current Radio Configuration

1. Open Anytone CPS
2. Connect your radio to the computer
3. Go to **Program → Read from Radio**
4. Save the current configuration as a backup: **File → Save As** → `original_codeplug.rtcfg`

### Step 2: Import Roaming Channels and Zones

1. Open CPS and go to the **Tool** menu → **Import**
2. Press the **Roaming Channel** button and pick the `RoamingChannel.CSV` file you downloaded
3. Press the **Roaming Zone** button and pick the `RoamingZone.CSV` file you downloaded
4. You should now see both files listed in the white file-selection box in the Import dialog
5. Click **Import** to bring the channels and zones into CPS
6. Verify the imports:
   - Channels: 35 entries with correct frequencies
   - Zones: 8 roaming zones with the correct member repeaters

Notes:
- On the AT‑D890, the roaming settings will be under the **DMR** section in CPS. Other Anytone models place roaming under a branch off the main tree; look for **Roaming Channels** and **Roaming Zones** in the left-hand navigation.
- Import order: import channels first, then zones if your CPS requires it. If both are imported together via the Import dialog, the tool will usually handle ordering automatically.

### Step 4: Write to Radio

1. Ensure your radio is connected via programming cable
2. Go to **Program → Write to Radio**
3. Wait for the write process to complete (may take several minutes)
4. Radio will restart automatically when complete

## Using Roaming on the Radio (Beginner Level)

### Select a Roaming Zone

Before you can roam, you must select which geographic zone you want to use:

```
Menu (White Button) → Scroll to Roaming → Select → 
[2] Roaming Zone → Select → Detroit Area → Select → 
Scroll to Select Zone → Select Button → 
(Displays "Detroit Area Selected") → Cancel (Red - - button)
```

**Available Zones:**
1. **Flint/Saginaw** - 8 repeaters covering Flint, Saginaw, and surrounding areas
2. **Thumb Area** - 3 repeaters covering the Michigan Thumb region
3. **Grand Rapids Area** - 5 repeaters covering Grand Rapids and west Michigan
4. **Lansing Area** - 2 repeaters covering Lansing and central Michigan
5. **Detroit Area** - 4 repeaters covering Detroit metro and southeast Michigan
6. **Lakeshore** - 4 repeaters covering Lake Michigan coastal areas
7. **Ann Arbor Area** - 2 repeaters covering Ann Arbor and Washtenaw County
8. **Northern Michigan** - 7 repeaters covering northern lower peninsula

### Activate One-Time Roaming

Once you've selected a zone, activate roaming to connect to the closest repeater:

```
Menu (White Button) → Scroll to Roaming → Select → 
[1] One Time Roaming → (Displays "Roaming Please Wait")
```

**What Happens:**
- Radio scans all repeaters in your selected zone
- Automatically selects the strongest signal
- Connects you to that repeater for transmission/reception
- You can now communicate on DMR talk groups

### Understanding Roam Mode Behavior

**Important: Roam Mode is Exclusive**

When you activate "One Time Roaming," the radio enters **exclusive roam mode** with these characteristics:

- **No Scanning**: Cannot use scan lists or channel scanning
- **No Manual Channel Selection**: Cannot switch to other channels
- **Automatic Operation**: Radio handles all repeater selection
- **Single Purpose**: Focused solely on finding and using the best repeater

**Visual Indicators:**
- Display shows "Roaming Please Wait" during scanning
- Once connected, shows the active repeater name/frequency
- Roam indicator appears on screen (varies by model)

**Return to Normal Operation:**
To exit roam mode and return to regular radio functions:

1. **Change Channel**: Select any other channel using channel knob or menu
2. **Re-enter Menu**: Simply accessing any menu function can exit roam mode
3. **Power Cycle**: Turn radio off and on (returns to last non-roaming state)

### Practical Usage Examples

**Traveling Between Cities:**
1. **Departure**: Select appropriate zone for your starting area
2. **En Route**: Activate roaming when approaching destination area
3. **Arrival**: Radio automatically connects to strongest local repeater
4. **Operation**: Communicate normally on DMR talk groups

**Best Practices:**
- **Zone Selection**: Choose the zone that best matches your current geographic area
- **Battery Life**: Roaming uses more battery than manual operation due to continuous scanning
- **Signal Quality**: If roaming fails, try manually selecting individual repeaters in the zone
- **Testing**: Test roaming in your home area before relying on it during travel

## Zone Coverage Details

### Flint/Saginaw Zone (8 repeaters)
**Coverage Areas:** Flint, Saginaw, Bay City, Midland
**Member Repeater List:** Bancroft, Bay City, Fenton, Flint, Frankenmuth, James TWP, Midland, Pinconning, Shepherd

### Thumb Area Zone (3 repeaters)
**Coverage Areas:** Michigan Thumb region
**Member Repeater List:** Burnside, Cass City, Mayville

### Grand Rapids Area Zone (5 repeaters)
**Coverage Areas:** Grand Rapids, west Michigan
**Member Repeater List:** Byron Center, Grand Rapids, Greenville, Lowell, Morley

### Lansing Area Zone (2 repeaters)
**Coverage Areas:** Lansing, central Michigan
**Member Repeater List:** Dansville, Lansing

### Detroit Area Zone (4 repeaters)
**Coverage Areas:** Detroit metro, southeast Michigan
**Member Repeater List:** Detroit, Mt.Clemens, Novi, Southgate

### Lakeshore Zone (4 repeaters)
**Coverage Areas:** Lake Michigan coastal areas
**Member Repeater List:** Grand Haven, Hamilton, Muskegon, West Olive

### Ann Arbor Area Zone (2 repeaters)
**Coverage Areas:** Ann Arbor, Washtenaw County
**Member Repeater List:** Grass Lake, Milan

### Northern Michigan Zone (7 repeaters)
**Coverage Areas:** Northern lower peninsula
**Member Repeater List:** Hackleburg, Lincoln, Mackinaw/Levering, Mio, Petoskey, Sault Ste. Marie

## Testing & Verification

### CPS Verification
1. **Check Channel Count**: Verify 35 channels imported successfully
2. **Zone Verification**: Confirm 8 zones with correct member repeaters
3. **Roaming Settings**: Ensure roaming is enabled with proper thresholds

### On-Radio Testing
1. **Zone Selection**: Select your local zone using the menu sequence above
2. **Roaming Test**: Activate "One Time Roaming" and verify connection to known repeater
3. **Communication Test**: Transmit on a local talk group (e.g., Michigan statewide TG 3129)
4. **Mobility Test**: If possible, test while moving within coverage area

### Expected Behavior
- **Successful Roam**: Radio connects within 10-30 seconds
- **Clear Signal**: Strong audio quality on connected repeater
- **Proper Identification**: Radio shows connected repeater name/frequency
## Closing

This guide is a short primer for using Anytone radios (primarily the AT‑D890) with CMEN repeaters in Michigan. It covers the on‑radio one‑time roaming workflow and how to import the provided CSV files into CPS. For full operational policies and etiquette, please refer to CMEN's site at https://w8cmn.net/dmr/. If you need more detail (advanced configuration, troubleshooting, or additional regions) please open an issue or pull request in this repository.
