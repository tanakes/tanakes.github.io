Let’s break down RAID simply. Think of RAID as a way to team up multiple hard drives (or SSDs) to act like one big drive, either for more speed, safety, or both.

I’ll start with the levels you’ll actually see in the real world (0, 1, 5, 6), then cover the ones that are now practically unused (2, 3, 4). Each explanation comes with a concrete example and a plain‑language analogy right after.

---

### RAID 0 – Striping (Speed, no safety)
**What it does:** Splits data into small chunks and writes them across all drives simultaneously. There’s no duplication, so you get the full combined capacity and very high read/write speed.  
**Example:** Two 1 TB drives in RAID 0 give you a single 2 TB volume. If either drive fails, **all data is lost**.  
**Analogy:** You and a friend copy a book by tearing it in half; each writes only their half at the same time. The copying is twice as fast. But if one notebook gets destroyed, the whole book is gone – the other half is useless.

---

### RAID 1 – Mirroring (Safety, no capacity gain)
**What it does:** Writes an identical copy of all data to two (or more) drives. You can read from any mirror, but write speed is limited by the slowest drive. Capacity is only the size of one drive.  
**Example:** Two 1 TB drives in RAID 1 give you 1 TB usable space. If one drive dies, the other holds a perfect copy, and you can replace the dead drive without losing anything.  
**Analogy:** You and a twin write down exactly the same notes simultaneously. If your notebook is lost, your twin’s notebook is an identical backup. The total unique information you can store is only what fits in one notebook, but you’re protected against the loss of a single notebook.

---

### RAID 5 – Striping with distributed parity (Good balance)
**What it does:** Needs at least 3 drives. Data is striped across drives, but it also calculates “parity” information – a kind of recovery formula – and spreads that parity across all drives. You can lose **any one drive** and still recover all data.  
**Example:** Three 1 TB drives give 2 TB usable (capacity = total minus one drive). If one drive dies, the array keeps working (though slower), and after you replace the failed drive the data is rebuilt automatically using the parity.  
**Analogy:** Three scribes copy a book. For every two pages of real text, they together create a “checksum page” (e.g., the sum of all letter positions). This checksum page is stored on a different scribe each time. If any single scribe loses all his pages, the other two can use their pages plus the checksums to mathematically reconstruct exactly what was lost.

---

### RAID 6 – Striping with double distributed parity (Extra safety)
**What it does:** Like RAID 5, but with **two independent parity calculations**. This means it can survive **two simultaneous drive failures**. It needs at least 4 drives.  
**Example:** Four 1 TB drives give 2 TB usable (capacity = total minus two drives). If any two drives die at once, all data is still safe and rebuildable.  
**Analogy:** Now our scribes create **two different** recovery pages for each batch of real pages – say a sum **and** a product. They distribute these extra pages among all scribes. Even if two scribes lose their complete notebooks, the remaining can still reconstruct everything from the remaining real pages and the two kinds of recovery data.

---

## The rarely used ones: RAID 2, 3, 4
These were designed long ago and are virtually never used in modern systems because they are either too complex, too slow, or solved problems that no longer exist.

### RAID 2 – Bit‑level striping with Hamming code
**What it does:** Splits data at the **bit level** across many data drives and uses additional drives to store a Hamming error‑correction code. This was meant to detect and correct errors on the fly.  
**Example:** A configuration might use 10 data disks and 4 ECC disks. If a drive returned bad data, the ECC could fix it instantly.  
**Why it’s unused:** Modern hard drives already have built‑in error correction (ECC) at the physical level. So adding another layer of bit‑level ECC across drives is redundant, plus it wastes a lot of drives and demands perfectly synchronized spindles.  
**Analogy:** You hire extra scribes solely to calculate and write a hyper‑detailed error‑correcting code for every single letter. But your pens already have a built‑in spell‑checker that never lets a bad letter through, so those extra scribes are completely unnecessary.

### RAID 3 – Byte‑level striping with a dedicated parity drive
**What it does:** Data is striped at the byte level across several data drives, and one drive is used exclusively to store parity.  
**Example:** Four 1 TB drives: three for data, one dedicated to parity. You get 3 TB usable. If a data drive fails, the parity drive helps rebuild it.  
**Why it’s unused:** Because every single write or read must touch the parity drive, that drive becomes a terrible bottleneck – it’s constantly busy while the data drives might be idle. RAID 5 solved this by spreading parity across all drives.  
**Analogy:** You have three writers and one person whose only job is to write the checksum for everything. Every time a writer changes a sentence, the checksum person must drop whatever they’re doing and update the recovery notes. That single person quickly becomes overwhelmed and slows everyone down.

### RAID 4 – Block‑level striping with a dedicated parity drive
**What it does:** Similar to RAID 3 but stripes data in larger blocks (sectors) instead of bytes, and still uses a single dedicated parity drive.  
**Example:** Same setup: 4×1 TB, 3 TB usable, one drive holds all parity. Small random writes suffer because the parity drive must be updated for every write, creating a bottleneck.  
**Why it’s unused:** The dedicated parity drive is still a single point of congestion for writes. RAID 5 distributes the parity blocks so no single drive becomes a hotspot, giving much better overall performance for the same usable capacity.  
**Analogy:** Now the writers hand over whole pages at a time to the checksum person. It’s a bit better than bytes, but that one person still has to process every page change while the writers wait. By rotating the checksum job among all members (RAID 5), nobody becomes the bottleneck.

---

In short, for any practical build today you’ll pick between RAID 0 (pure speed, no safety), RAID 1 (pure mirroring), RAID 5 (single‑drive failure protection with good speed/capacity), or RAID 6 (dual‑drive failure protection). The levels 2, 3, and 4 are historical footnotes that have been replaced by better designs and modern drive technology.