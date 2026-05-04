# AOG Conduit Fill Calculator

A professional NEC Chapter 9 compliant conduit fill calculator built for electrical contractors and field technicians.

## Features

✨ **NEC 2023 Compliance**
- Table 1: Percent conduit fill rules (53%, 31%, 40%, 60%)
- Table 4: Conduit internal dimensions & areas
- Table 5: Conductor cross-sectional areas by type/size
- Jam ratio prediction (NEC informational note)

⚡ **Comprehensive Wire Database**
- 15+ conductor types (THHN, THWN-2, XHHW, RHH/RHW, USE-2, TW/THW, MTW, PFA, TFN, ZW, Bare)
- Wire sizes from 14 AWG to 1000 kcmil
- Accurate outer diameter (OD) measurements for jam calculations

🏗️ **Conduit Support**
- RMC, IMC, EMT, FMC, LFMC
- LFNC-A & LFNC-B (Liquidtight Flexible Nonmetallic)
- PVC Schedule 40 & 80
- HDPE, ENT
- Trade sizes: 3/8" through 6"

🔧 **Smart Calculations**
- **Raceway Mode**: 40% fill (or 53%/31% for 1-2 conductors)
- **Nipple Mode**: 60% fill (for runs ≤24")
- Real-time fill percentage tracking
- Visual fill bar with color coding (green/yellow/red)
- Best fit recommendation (smallest conduit that passes)
- Jam ratio analysis for 3+ conductors
- Fill headroom calculation

🎨 **User Experience**
- Dark/light theme toggle with localStorage persistence
- Responsive mobile-friendly design
- Smooth animations and transitions
- Print-friendly layouts
- Real-time updates as you add/remove conductors
- Conduit info preview (ID, total area, allowed fill)

📊 **Detailed Results**
- Wire summary chips showing all conductors
- All conduit sizes table with pass/fail status
- Fill visualization for each size
- Jam ratio grid with risk assessment (low/moderate/high)
- Copy-paste friendly results

## Getting Started

### Quick Start
1. Open `index.html` in any modern web browser
2. Select conduit type and trade size
3. Add conductors (wire type, size, quantity)
4. Click "CALCULATE CONDUIT FILL"
5. Review results and recommendations

### No Installation Required
This is a standalone HTML/CSS/JavaScript application. Simply save and open in your browser. Works offline.

## Usage Examples

### Example 1: Three 12 AWG THHN in EMT
1. Select **EMT** conduit type
2. Leave trade size blank (calculator shows all sizes)
3. Add 3 conductors:
   - Wire Type: THHN/THWN-2
   - Size: 12 AWG
   - Qty: 1 (repeat 3 times)
4. Click Calculate
5. **Result**: 1/2" EMT passes at ~43% fill (40% rule for 3+ conductors)

### Example 2: Mixed Gauge Feeder
1. Select **RMC** conduit type
2. Select **2"** trade size
3. Add conductors:
   - 2× 2/0 AWG THHN/THWN-2 (hots)
   - 1× 2/0 AWG THHN/THWN-2 (neutral)
   - 1× 4 AWG Bare Conductor (ground)
4. Click Calculate
5. Review fill percentage and jam ratio

## Data Sources

- **NEC 2023** (National Electrical Code)
  - Table 1: Percent Conduit Fill
  - Table 4: Conduit and Tubing Physical Dimensions
  - Table 5: Conductor Properties
  - Informational Note: Jam Ratio Formula

- **Wire OD measurements**: NEC Table 5 annotations and UL standards

## Technical Details

### Architecture
- **No dependencies**: Pure HTML5, CSS3, JavaScript
- **Data structure**: Nested objects for O(1) lookups
- **State management**: Simple JavaScript variables with localStorage for theme

### Browser Support
- Chrome/Edge 90+
- Firefox 88+
- Safari 14+
- Mobile browsers (iOS Safari, Chrome Mobile)

### Key Functions
- `calculate()`: Main calculation engine
- `getAllowedFillPct()`: NEC Table 1 fill percentage lookup
- `renderJamRatios()`: Jam ratio analysis for 3+ conductors
- `addWire() / removeWire()`: Dynamic conductor management
- `toggleTheme()`: Dark mode with persistence

## File Structure

```
index.html              # Complete application (single file)
├── <head>
│   ├── Fonts (Google Fonts: Orbitron, Share Tech Mono, Exo 2)
│   └── <style> (1200+ lines of responsive CSS)
├── <body>
│   ├── Header (branding, theme toggle, NEC badge)
│   ├── Main content
│   │   ├── Raceway type selector (40% vs 60% nipple)
│   │   ├── Conduit type & size selection
│   │   ├── Dynamic conductor input
│   │   └── Calculate button
│   ├── Results section (hidden until calculate)
│   │   ├── Fill summary stats
│   │   ├── All sizes table
│   │   └── Jam ratio grid
│   └── Footer (credits)
└── <script> (900+ lines)
    ├── CONDUIT_DATA (NEC Table 4)
    ├── WIRE_DATA (NEC Table 5)
    └── Function library
```

## NEC Rules Reference

### Table 1 — Percent Conduit Fill
| # Conductors | Fill % |
|---|---|
| 1 | 53% |
| 2 | 31% |
| 3+ | 40% |
| Nipple (≤24") | 60% |

### Jam Ratio (NEC Informational Note)
- **Ratio Formula**: Conduit ID ÷ Largest Wire OD
- **Low Risk**: Ratio > 3.2 (plenty of space)
- **Moderate Risk**: Ratio 3.2–3.8 (use caution)
- **High Risk**: Ratio 2.8–3.2 (avoid if possible)
- **Too Small**: Ratio < 2.8 (conductor won't fit)

## Customization

### Add a Wire Type
Edit `WIRE_DATA` object:
```javascript
"Your Wire Type": {
  "14 AWG": { area: 0.0139, od: 0.133 },
  "12 AWG": { area: 0.0181, od: 0.152 },
  // ... more sizes
}
```

### Add a Conduit Size
Edit `CONDUIT_DATA` object:
```javascript
RMC: {
  "3/8": { id: 0.493, total: 0.191 },
  // ... more sizes
}
```

### Change Colors
Modify CSS custom properties in `:root`:
```css
:root {
  --accent: #D97706;        /* Primary accent (orange) */
  --success: #059669;       /* Green (pass) */
  --danger: #DC2626;        /* Red (fail) */
  --warn: #d97706;          /* Yellow/orange (warning) */
}
```

## Known Limitations

- Single-run calculations only (no parallel runs)
- No derating for temperature or altitude
- Jam ratio calculation requires 3+ conductors
- No support for metric sizes (imperial only)
- Nipple mode assumes ≤24" run (user responsible for verification)

## Future Enhancements

- [ ] Export to PDF/print-optimized report
- [ ] Save/load calculation history
- [ ] Multi-run feeder sizing
- [ ] Metric conduit sizes
- [ ] NEC 2026 updates
- [ ] Resistance/voltage drop calculations
- [ ] PWM compatible wire sizing

## Credits

**Built by**: Brandon @ AOG Field Operations Hub  
**Based on**: NEC 2023 Chapter 9 (NFPA 70)  
**License**: Open source for field use

## Support

For bug reports or feature requests, contact: [Your contact info]

## Disclaimer

This calculator is a design aid. Always verify calculations against current NEC code and applicable local electrical codes. Consult a licensed electrician or engineer for critical installations.

---

**Last Updated**: 2024  
**NEC Edition**: 2023  
**Status**: Production Ready ✅
