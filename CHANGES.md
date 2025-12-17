# Quickshell Bar Configuration Changes

## Summary
Konfigurasi bar Quickshell telah dimodifikasi untuk menyederhanakan tampilan dengan menyembunyikan elemen yang tidak diperlukan dan membuat layout lebih dinamis.

---

## Changes Made

### 1. Resource Indicators (CPU Only)
**File:** `ii/modules/ii/bar/Resources.qml`

Menyembunyikan indicator Memory (RAM) dan Swap, hanya menampilkan CPU:

```qml
Resource {
    visible: false  // Hidden - only showing CPU
    iconName: "memory"
    ...
}

Resource {
    visible: false  // Hidden - only showing CPU
    iconName: "swap_horiz"
    ...
}

Resource {
    iconName: "planner_review"
    shown: true  // Always show CPU
    Layout.leftMargin: 0
    ...
}
```

---

### 2. Dynamic Media Control
**File:** `ii/modules/ii/bar/BarContent.qml`

Media control disembunyikan ketika tidak ada media yang diputar:

```qml
Media {
    visible: root.useShortenedForm < 2 && MprisController.activePlayer != null
    Layout.fillWidth: true
}
```

---

### 3. Dynamic Width for Resource Group
**File:** `ii/modules/ii/bar/BarContent.qml`

Lebar area resource/media menyesuaikan konten untuk menghindari gap kosong:

```qml
BarGroup {
    id: leftCenterGroup
    // Dynamic width: full width when media is playing, auto-fit when not
    implicitWidth: (MprisController.activePlayer != null) ? root.centerSideModuleWidth : resourcesItem.implicitWidth + 16

    Resources {
        id: resourcesItem
        ...
    }
    ...
}
```

---

### 4. Battery Indicator Moved to Right Group
**File:** `ii/modules/ii/bar/BarContent.qml`

Battery indicator dipindahkan dari grup tengah ke grup indicator kanan (bersama network/bluetooth):

```qml
// Di rightCenterGroup (posisi lama) - disembunyikan
BatteryIndicator {
    visible: false  // Moved to right indicator group
    ...
}

// Di indicatorsRowLayout (posisi baru) - paling kiri dalam grup
BatteryIndicator {
    Layout.rightMargin: indicatorsRowLayout.realSpacing
    visible: Battery.available
    Layout.alignment: Qt.AlignVCenter
    Layout.preferredHeight: Appearance.font.pixelSize.larger
    scale: 0.8
}
```

---

### 5. Workspace Moved to Right of Middle Section
**File:** `ii/modules/ii/bar/BarContent.qml`

Urutan komponen di tengah bar diubah:
- **Sebelum:** CPU → Workspaces → Clock
- **Sesudah:** CPU → Clock → Workspaces

---

### 6. Time/Date Width Auto-fit
**File:** `ii/modules/ii/bar/BarContent.qml`

Lebar area time/date menyesuaikan kontennya:

```qml
MouseArea {
    id: rightCenterGroup
    implicitWidth: rightCenterGroupContent.implicitWidth  // Auto-fit to content
    ...
}
```

---

## Result

| Area | Tampilan |
|------|----------|
| Kiri | LeftSidebarButton, ActiveWindow |
| Tengah | CPU indicator, Clock/Date, Workspaces |
| Kanan | Battery, Volume/Mic, Network, Bluetooth |

| Kondisi | Behavior |
|---------|----------|
| Ada media aktif | CPU + Media control (lebar penuh) |
| Tidak ada media | CPU saja (lebar menyesuaikan) |

---

## Files Modified

1. `ii/modules/ii/bar/Resources.qml` - Hide RAM/Swap, show CPU only
2. `ii/modules/ii/bar/BarContent.qml` - Multiple layout changes
