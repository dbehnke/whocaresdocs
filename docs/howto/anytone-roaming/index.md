# Anytone DMR Roaming Guide

This guide explains how to set up and use DMR roaming with Anytone radios, focusing on the Anytone 890 handheld with compatibility notes for the 578 mobile and 168 handheld models. The provided files cover Michigan-area repeaters for automatic roaming operation.

## What is DMR Roaming?

DMR roaming allows your radio to automatically select the strongest repeater from a predefined group when you're traveling or in areas with multiple repeaters. Instead of manually switching channels, the radio scans for the best signal and connects you automatically.

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

Right-click and save these files to your computer:

- [**RoamingZone.CSV**](anytone-roaming/RoamingZone.CSV) - Zone definitions (8 zones)
- [**RoamingChannel.CSV**](anytone-roaming/RoamingChannel.CSV) - Repeater details (35 repeaters)

**File Verification:**
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
3. Go to **Programmer → Read from Radio**
4. Save the current configuration as a backup: **File → Save As** → `original_codeplug.rtcfg`

### Step 2: Import Roaming Channels

1. In CPS, go to the **Digital** tab or **Channel** section
2. Look for **Import** or **Import from CSV** option
3. Select **RoamingChannel.CSV** that you downloaded
4. Verify that 35 new channels are imported with proper frequencies
5. Check that all channels use:
   - Color Code: 1
   - Slot: Slot 1
   - Frequency range: 442-445 MHz (UHF)

### Step 3: Import Roaming Zones

1. In CPS, navigate to the **Roaming** or **Roaming Zone** section
2. Select **Import** or **Import from CSV**
3. Choose **RoamingZone.CSV** that you downloaded
4. Verify that 8 roaming zones are imported with proper names
5. Check that each zone contains the correct member repeaters

### Step 4: Configure Roaming Settings

1. In the **Roaming** section, verify:
   - Roaming is enabled
   - Proper scan priorities are set
   - RSSI thresholds are reasonable (typically -100 to -110 dBm)
2. Save your configuration: **File → Save** → `michigan_roaming_codeplug.rtcfg`

### Step 5: Write to Radio

1. Ensure your radio is connected via programming cable
2. Go to **Programmer → Write to Radio**
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

## Compatibility Notes

### Anytone 578 Mobile Radio
- **CPS Differences**: Menu layout varies but functionality is similar
- **Button Mapping**: Different physical buttons but same logical sequence
- **Power Considerations**: Mobile installation provides better antenna performance

### Anytone 168 Handheld
- **Limited Features**: May have simplified roaming interface
- **Screen Size**: Smaller display may show limited information
- **Battery Life**: Similar battery consumption during roaming

### CPS Version Compatibility
- **Always Match**: Use CPS version matching your radio's firmware
- **Update Firmware**: Update firmware before updating CPS if needed
- **Backup First**: Always backup original configuration before making changes

## Troubleshooting

### Common Roaming Issues

**"No Signal Found"**
- **Check Zone**: Verify you selected the correct geographic zone
- **Range Issues**: You may be outside coverage of all zone repeaters
- **Antenna**: Ensure antenna is properly connected and undamaged

**"Roaming Failed"**
- **Interference**: High RF interference may prevent signal detection
- **Settings**: Check RSSI thresholds in CPS (try -100 dBm if set too high)
- **Firmware**: Update radio firmware and CPS to latest versions

**Poor Audio Quality**
- **Signal Strength**: Weak signal to selected repeater
- **Manual Override**: Try manually selecting individual repeaters in the zone
- **Interference**: Check for local RF interference sources

### File Import Issues

**CSV Import Errors**
- **File Format**: Ensure files weren't modified or corrupted
- **CPS Version**: Verify CPS version supports CSV import for roaming
- **File Location**: Use the original files from this guide

**Missing Channels**
- **Import Order**: Import channels first, then zones
- **Verify Count**: Should see exactly 35 channels and 8 zones
- **Re-import**: If issues occur, start over with fresh CPS session

### Performance Optimization

**Battery Life During Roaming**
- **Limit Duration**: Use roaming only when needed, not continuously
- **Power Save**: Enable power save features when not roaming
- **Battery Condition**: Use fresh or fully charged battery for travel

**Signal Quality**
- **Antenna Upgrade**: Consider aftermarket antenna for better performance
- **Location**: Higher elevation provides better coverage
- **Avoid Obstructions**: Buildings and terrain can block signals

## Advanced Configuration

### Custom Zone Creation
1. **Open CPS**: Access roaming zone configuration
2. **Create New Zone**: Define zone name and geographic area
3. **Add Channels**: Select individual repeaters to include
4. **Set Priorities**: Configure scanning order and RSSI thresholds

### Adding New Repeaters
1. **Update Channel List**: Add new repeater frequencies to channel database
2. **Configure Zones**: Add new repeaters to appropriate zones
3. **Test thoroughly**: Verify new repeaters work correctly in roam mode

### Roaming Priorities
1. **RSSI Thresholds**: Set minimum signal strength (-100 to -110 dBm typical)
2. **Scan Order**: Prioritize preferred repeaters within zones
3. **Hold Times**: Configure how long to stay on selected repeater

## Technical Specifications

### Repeater Technical Details
All 35 repeaters in the database use these standardized settings:

- **Frequency Range:** 442.0000 - 444.9500 MHz (UHF band)
- **Color Code:** 1 (all repeaters)
- **Timeslot:** Slot 1 (all repeaters)
- **Power:** Various (5-50W depending on repeater)
- **Digital Mode:** DMR Tier II
- **Analog Fallback:** Not supported (digital only)

### Coverage Notes
- **Michigan Focus:** Optimized for Michigan amateur radio operators
- **Urban Coverage:** Strong coverage in major metropolitan areas
- **Rural Coverage:** Limited in remote areas (repeater dependent)
- **Interoperability:** Compatible with all standard DMR radios

## Getting Help

If you encounter issues not covered in this guide:

1. **Local Amateur Radio Clubs:** Contact your local club for Michigan-specific advice
2. **Anytone Support:** Official Anytone technical support for CPS/radio issues
3. **Online Communities:** DMR forums and groups for roaming discussions
4. **Repeater Owners:** Contact individual repeater owners for specific site issues

---

**Version 1.0** - Created for Whocares Amateur Radio Group documentation

*This guide covers DMR roaming setup and operation for Anytone radios with Michigan-area repeaters. Adapt as needed for other regions or radio models.*