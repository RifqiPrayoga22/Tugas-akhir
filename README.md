<!DOCTYPE html>
<html lang="id">
<head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <title>Sistem Pendataan Barang di Gudang (OOP)</title>
    <!-- Mermaid.js -->
    <script src="https://cdn.jsdelivr.net/npm/mermaid@10/dist/mermaid.min.js">
    </script>
    <style>
        /* ─── RESET & GLOBAL ─── */
        * {
            margin: 0;
            padding: 0;
            box-sizing: border-box;
        }

        body {
            font-family: 'Segoe UI', 'Courier New', monospace;
            background: #0b1120;
            color: #e2e8f0;
            min-height: 100vh;
            line-height: 1.6;
        }

        .container {
            max-width: 1300px;
            margin: 0 auto;
            padding: 15px 20px;
        }

        /* ─── HEADER ─── */
        .header {
            background: linear-gradient(135deg, #0f172a, #1e293b);
            border-bottom: 2px solid #38bdf8;
            padding: 25px 20px;
            text-align: center;
            border-radius: 0 0 20px 20px;
            margin-bottom: 20px;
        }

        .header h1 {
            font-size: 2.2em;
            background: linear-gradient(90deg, #38bdf8, #818cf8);
            -webkit-background-clip: text;
            background-clip: text;
            color: transparent;
            text-shadow: 0 0 20px rgba(56, 189, 248, 0.3);
        }

        .header .subtitle {
            color: #94a3b8;
            font-size: 1.1em;
            margin-top: 4px;
        }

        .header .identitas {
            margin-top: 12px;
            padding: 10px;
            background: rgba(56, 189, 248, 0.05);
            border-radius: 12px;
            display: inline-block;
        }

        .header .identitas h3 {
            color: #818cf8;
        }

        .header .identitas p {
            color: #cbd5e1;
            margin: 2px 0;
        }

        .header hr {
            width: 60%;
            max-width: 400px;
            margin: 16px auto;
            border: none;
            height: 2px;
            background: linear-gradient(90deg, #38bdf8, #818cf8);
            border-radius: 2px;
        }

        /* ─── SECTIONS ─── */
        .section {
            margin: 24px 0;
            padding: 22px 24px;
            border-radius: 16px;
            background: rgba(15, 23, 42, 0.85);
            border: 1px solid rgba(56, 189, 248, 0.2);
            backdrop-filter: blur(8px);
            transition: all 0.3s ease;
        }

        .section:hover {
            border-color: #818cf8;
            box-shadow: 0 0 30px rgba(129, 140, 248, 0.15);
        }

        .section h2 {
            color: #38bdf8;
            font-size: 1.5em;
            margin-bottom: 12px;
            display: flex;
            align-items: center;
            gap: 10px;
        }

        .section h2::after {
            content: "";
            flex: 1;
            height: 2px;
            background: linear-gradient(90deg, #38bdf8, transparent);
        }

        .section h3 {
            color: #818cf8;
            margin: 16px 0 8px 0;
        }

        .section p,
        .section li {
            color: #cbd5e1;
        }

        .section b {
            color: #fbbf24;
        }

        /* ─── CARDS ─── */
        .card {
            background: rgba(2, 6, 23, 0.6);
            border: 1px solid rgba(56, 189, 248, 0.15);
            border-radius: 12px;
            padding: 16px 18px;
            transition: all 0.3s ease;
        }

        .card:hover {
            border-color: #818cf8;
            transform: translateY(-2px);
        }

        .card .card-title {
            font-weight: bold;
            color: #fbbf24;
            font-size: 1em;
            margin-bottom: 6px;
        }

        .card .card-sub {
            color: #94a3b8;
            font-size: 0.85em;
        }

        /* ─── FORM ROW ─── */
        .form-row {
            display: flex;
            flex-wrap: wrap;
            gap: 10px 14px;
            align-items: center;
            margin-top: 8px;
        }

        .form-row label {
            color: #94a3b8;
            font-size: 0.85em;
            min-width: 70px;
        }

        .form-row input,
        .form-row select {
            background: rgba(2, 6, 23, 0.8);
            border: 1px solid rgba(56, 189, 248, 0.3);
            border-radius: 8px;
            padding: 8px 14px;
            color: #e2e8f0;
            font-family: inherit;
            font-size: 0.9em;
            flex: 1;
            min-width: 120px;
        }

        .form-row input:focus,
        .form-row select:focus {
            outline: none;
            border-color: #818cf8;
            box-shadow: 0 0 15px rgba(129, 140, 248, 0.2);
        }

        /* ─── BUTTONS ─── */
        .btn {
            padding: 8px 18px;
            border: none;
            border-radius: 8px;
            font-weight: 600;
            font-family: inherit;
            font-size: 0.8em;
            cursor: pointer;
            transition: all 0.3s ease;
            color: #fff;
            background: linear-gradient(135deg, #38bdf8, #818cf8);
            box-shadow: 0 4px 15px rgba(56, 189, 248, 0.3);
        }

        .btn:hover {
            transform: scale(1.05);
            box-shadow: 0 6px 25px rgba(56, 189, 248, 0.5);
        }

        .btn.small {
            padding: 5px 12px;
            font-size: 0.7em;
        }
        .btn.green {
            background: linear-gradient(135deg, #34d399, #22d3ee);
        }
        .btn.orange {
            background: linear-gradient(135deg, #fb923c, #facc15);
        }
        .btn.red {
            background: linear-gradient(135deg, #f87171, #fb923c);
        }
        .btn.purple {
            background: linear-gradient(135deg, #818cf8, #a78bfa);
        }
        .btn.cyan {
            background: linear-gradient(135deg, #22d3ee, #67e8f9);
            color: #0f172a;
        }
        .btn.outline {
            background: transparent;
            border: 1px solid #38bdf8;
            color: #38bdf8;
            box-shadow: none;
        }
        .btn.outline:hover {
            background: rgba(56, 189, 248, 0.1);
        }

        /* ─── GRID ─── */
        .grid-2 {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
        }
        .grid-3 {
            display: grid;
            grid-template-columns: repeat(3, 1fr);
            gap: 18px;
        }

        @media (max-width: 768px) {
            .grid-2,
            .grid-3 {
                grid-template-columns: 1fr;
            }
            .section {
                padding: 16px;
            }
            .section h2 {
                font-size: 1.2em;
            }
        }

        /* ─── TERMINAL ─── */
        .terminal {
            background: #020617;
            border: 1px solid #38bdf8;
            border-radius: 12px;
            padding: 14px 18px;
            max-height: 350px;
            overflow-y: auto;
            font-size: 0.8em;
            line-height: 1.8;
            color: #cbd5e1;
            margin-top: 10px;
            font-family: 'Courier New', monospace;
        }

        .terminal .log-line {
            padding: 2px 0;
            border-bottom: 1px solid rgba(56, 189, 248, 0.05);
        }

        .terminal .log-line .time {
            color: #475569;
            margin-right: 12px;
        }
        .terminal .log-line .green {
            color: #34d399;
        }
        .terminal .log-line .red {
            color: #f87171;
        }
        .terminal .log-line .cyan {
            color: #22d3ee;
        }
        .terminal .log-line .gray {
            color: #94a3b8;
        }
        .terminal .log-line .yellow {
            color: #fbbf24;
        }
        .terminal .log-line .purple {
            color: #818cf8;
        }

        /* ─── MERMAID ─── */
        .mermaid-wrapper {
            background: rgba(2, 6, 23, 0.6);
            border-radius: 12px;
            padding: 16px;
            overflow: auto;
            border: 1px solid rgba(56, 189, 248, 0.1);
            margin-top: 10px;
        }

        .mermaid-wrapper .mermaid {
            display: flex;
            justify-content: center;
            min-width: 100%;
        }

        .mermaid-wrapper .mermaid svg {
            max-width: 100%;
            height: auto;
        }

        /* ─── CODE BLOCK ─── */
        .code-block {
            background: #020617;
            border-left: 3px solid #818cf8;
            padding: 14px 18px;
            border-radius: 0 8px 8px 0;
            font-size: 0.8em;
            white-space: pre-wrap;
            word-break: break-word;
            color: #cbd5e1;
            margin-top: 12px;
            overflow-x: auto;
            max-height: 400px;
            overflow-y: auto;
            display: none;
            font-family: 'Courier New', monospace;
        }

        .code-block.show {
            display: block;
        }

        .code-block .label {
            color: #818cf8;
            font-weight: bold;
            display: block;
            margin-bottom: 6px;
        }

        .copy-btn {
            background: rgba(129, 140, 248, 0.15);
            border: 1px solid #818cf8;
            color: #818cf8;
            padding: 6px 16px;
            border-radius: 6px;
            font-family: inherit;
            font-size: 0.75em;
            cursor: pointer;
            transition: 0.3s;
        }

        .copy-btn:hover {
            background: rgba(129, 140, 248, 0.3);
            box-shadow: 0 0 20px rgba(129, 140, 248, 0.2);
        }

        .copy-section {
            display: flex;
            gap: 10px;
            flex-wrap: wrap;
            margin-top: 10px;
        }

        /* ─── OOP PILLARS ─── */
        .pillar-card {
            border-left: 4px solid #818cf8;
            padding: 12px 16px;
            background: rgba(2, 6, 23, 0.4);
            border-radius: 0 8px 8px 0;
        }

        .pillar-card h4 {
            color: #fbbf24;
            font-size: 1em;
        }

        .pillar-card p {
            font-size: 0.85em;
            color: #cbd5e1;
        }

        /* ─── FOOTER ─── */
        footer {
            text-align: center;
            padding: 25px;
            color: #94a3b8;
            font-size: 0.85em;
            border-top: 1px solid rgba(56, 189, 248, 0.15);
            margin-top: 30px;
        }

        .spacer {
            height: 30px;
        }

        /* ─── DARTPAD ─── */
        iframe {
            margin-top: 10px;
            max-width: 100%;
            height: 500px;
            display: none;
            border-radius: 10px;
            border: 1px solid rgba(56, 189, 248, 0.3);
            background: #020617;
            width: 100%;
        }

        .dartpad-row {
            display: flex;
            flex-wrap: wrap;
            gap: 12px;
            align-items: center;
            margin-top: 8px;
        }

        /* ─── BADGE ─── */
        .badge {
            display: inline-block;
            padding: 2px 12px;
            border-radius: 20px;
            font-size: 0.7em;
            font-weight: 600;
        }
        .badge.available {
            background: rgba(52, 211, 153, 0.2);
            color: #34d399;
            border: 1px solid #34d399;
        }
        .badge.rented {
            background: rgba(248, 113, 113, 0.2);
            color: #f87171;
            border: 1px solid #f87171;
        }

        /* ─── PSEUDOCODE STYLING ─── */
        .pseudocode-container {
            display: grid;
            grid-template-columns: 1fr 1fr;
            gap: 20px;
            margin-top: 8px;
        }

        .pseudocode-box {
            background: rgba(2, 6, 23, 0.8);
            border-radius: 8px;
            padding: 16px 18px;
            border-left: 4px solid #fbbf24;
            font-family: 'Courier New', monospace;
            font-size: 0.75em;
            color: #cbd5e1;
            line-height: 1.8;
            overflow-x: auto;
        }

        .pseudocode-box h5 {
            color: #fbbf24;
            font-size: 1.1em;
            margin-bottom: 8px;
            font-family: 'Segoe UI', sans-serif;
        }

        .pseudocode-box .keyword {
            color: #fbbf24;
            font-weight: bold;
        }

        .pseudocode-box .input {
            color: #818cf8;
        }

        .pseudocode-box .output {
            color: #34d399;
        }

        .pseudocode-box .error {
            color: #f87171;
        }

        .pseudocode-box .comment {
            color: #64748b;
            font-style: italic;
        }

        /* ─── SOURCE CODE STYLING ─── */
        .source-code-container {
            background: #0a0a1a;
            border-radius: 12px;
            padding: 20px;
            border: 1px solid #38bdf8;
            margin-top: 12px;
            max-height: 600px;
            overflow-y: auto;
            font-family: 'Courier New', monospace;
            font-size: 0.75em;
            line-height: 1.8;
            color: #cbd5e1;
            white-space: pre-wrap;
            word-break: break-word;
        }

        .source-code-container .line-number {
            display: inline-block;
            width: 30px;
            color: #475569;
            user-select: none;
        }

        .source-code-container .keyword {
            color: #818cf8;
            font-weight: bold;
        }

        .source-code-container .string {
            color: #34d399;
        }

        .source-code-container .comment {
            color: #64748b;
            font-style: italic;
        }

        .source-code-container .class-name {
            color: #fbbf24;
        }

        .source-code-container .method {
            color: #22d3ee;
        }

        .source-code-container .type {
            color: #a78bfa;
        }

        .source-code-container .number {
            color: #fb923c;
        }

        .source-code-container .operator {
            color: #f472b6;
        }

        .source-code-container .punctuation {
            color: #94a3b8;
        }

        .source-code-container .variable {
            color: #e2e8f0;
        }

        .source-code-container .function {
            color: #facc15;
        }

        @media (max-width: 768px) {
            .pseudocode-container {
                grid-template-columns: 1fr;
            }
        }
    </style>
</head>

<body>

    <!-- HEADER -->
    <header class="header">
        <h1>Sistem Pendataan Barang di Gudang</h1>
        <div class="subtitle">Tugas Kelompok: Penerapan OOP (Bab 10)</div>
        <hr />
        <div class="identitas">
            <h3>ANGGOTA KELOMPOK</h3>
            <p>Yoza Ulpia Rafila - 251410004 - SI2A</p>
            <p>Rifqi Prayoga - 251410005 - SI2A</p>
        </div>
    </header>

    <div class="container">

        <!-- DASHBOARD & KONTROL GUDANG -->
        <div class="section">
            <h2>Dashboard & Kontrol Gudang</h2>

            <div class="card" style="border-color:#818cf8;">
                <div class="card-title">Tambah Barang Baru ke Gudang</div>
                <div class="form-row">
                    <label>Kode</label>
                    <input type="text" id="newKode" value="BRG-001" />
                    <label>Nama</label>
                    <input type="text" id="newNama" value="Laptop Asus" />
                    <label>Kategori</label>
                    <input type="text" id="newKategori" value="Elektronik" />
                    <label>Stok</label>
                    <input type="number" id="newStok" value="10" />
                    <button class="btn green" onclick="tambahBarang()">Tambah</button>
                </div>
            </div>

            <div class="card" style="margin-top:14px; border-color:#38bdf8;">
                <div class="card-title">Pilih Barang & Kelola Stok</div>
                <div class="form-row">
                    <label>Pilih Barang</label>
                    <select id="selectBarang"></select>
                    <button class="btn cyan small" onclick="refreshSelect()">Refresh</button>
                </div>
                <div class="form-row" style="margin-top:8px;">
                    <button class="btn green small" onclick="tambahStok()">Tambah Stok</button>
                    <button class="btn orange small" onclick="kurangiStok()">Kurangi Stok</button>
                    <button class="btn purple small" onclick="tampilkanBarang()">Detail</button>
                    <button class="btn red small" onclick="hapusBarang()">Hapus</button>
                </div>
                <div style="margin-top:8px; font-size:0.85em; color:#94a3b8;">
                    <span id="infoBarang">Belum ada barang dipilih.</span>
                </div>
            </div>
        </div>

        <!-- DAFTAR BARANG -->
        <div class="section">
            <h2>Daftar Barang di Gudang</h2>
            <div id="inventoryGrid" class="grid-3"></div>
        </div>

        <!-- TERMINAL -->
        <div class="section" style="border-color:#818cf8;">
            <h2 style="color:#818cf8 !important;">Terminal Console</h2>
            <div class="terminal" id="terminal">
                <div class="log-line"><span class="time">[INIT]</span> <span class="cyan">Sistem Pendataan Barang di Gudang</span> <span class="gray">siap digunakan.</span></div>
                <div class="log-line"><span class="time">[INIT]</span> <span class="green">5 barang contoh berhasil di-instansiasi.</span></div>
                <div class="log-line"><span class="time">[INIT]</span> <span class="yellow">Total barang di gudang: 5 unit.</span></div>
            </div>
            <button class="btn small outline" onclick="clearTerminal()" style="margin-top:8px;">Clear Log</button>
            <button class="btn small outline" onclick="simulasiTransaksi()" style="margin-top:8px; margin-left:8px;">Jalankan Simulasi 10 Transaksi</button>
        </div>

        <!-- LOGIKA & DIAGRAM SISTEM -->
        <div class="section" style="border:2px solid rgba(56,189,248,0.3);">
            <h2 style="color:#38bdf8 !important;">LOGIKA & DIAGRAM SISTEM</h2>
            <p style="color:#94a3b8; font-size:0.9em; margin-bottom:6px;">
                Visualisasi logika OOP & alur kerja sistem pendataan barang di gudang.
            </p>

            <!-- DIAGRAM 1: CLASS DIAGRAM (UML) -->
            <h3 style="color:#818cf8; margin-top:16px;">DIAGRAM KELAS (UML)</h3>
            <p style="color:#94a3b8; font-size:0.85em; margin-bottom:6px;">
                Menunjukkan arsitektur kelas OOP (Inheritance, Association, dan Dependency) beserta atribut dan metode masing-masing kelas.
            </p>

            <div class="mermaid-wrapper">
                <div class="mermaid">
                    classDiagram
                    direction TB

                    class EntitasGudang {
                        &lt;&lt;abstract&gt;&gt;
                        -String kode
                        -String nama
                        +EntitasGudang(kode nama)
                        +tampilkanInfo() void
                        +cetakIdentitas() void
                    }

                    class Barang {
                        -String kategori
                        -String merk
                        -int jumlahStok
                        -String satuan
                        -String kondisi
                        +Barang(kode nama kategori merk stok satuan kondisi)
                        +tampilkanInfo() void
                        +tambahStok(jumlah) bool
                        +kurangiStok(jumlah) bool
                        +getStok() int
                    }

                    class Gudang {
                        -List~Barang~ daftarBarang
                        -List~Transaksi~ riwayatTransaksi
                        -Map~StringStokBarang~ stokBarang
                        +Gudang()
                        +tambahBarang(barang) void
                        +cariBarang(kode) Barang
                        +tambahStok(kode jumlah) bool
                        +kurangiStok(kode jumlah) bool
                        +tampilkanSemuaBarang() void
                        +getTotalBarang() int
                        +init() void
                        +simulasiTransaksi() void
                    }

                    class Transaksi {
                        &lt;&lt;abstract&gt;&gt;
                        -String idTransaksi
                        -String tanggal
                        -String kodeBarang
                        -int jumlah
                        +Transaksi(id tanggal kode jumlah)
                        +prosesTransaksi() void
                        +cetakHeader() void
                    }

                    class BarangMasuk {
                        -String namaSupplier
                        +BarangMasuk(id tanggal kode jumlah supplier)
                        +prosesTransaksi() void
                    }

                    class BarangKeluar {
                        -String tujuan
                        +BarangKeluar(id tanggal kode jumlah tujuan)
                        +prosesTransaksi() void
                    }

                    class StokBarang {
                        -int stokAwal
                        -int barangMasuk
                        -int barangKeluar
                        -int stokAkhir
                        -String status
                        +StokBarang(stokAwal)
                        +tambahMasuk(jumlah) void
                        +tambahKeluar(jumlah) void
                        +hitungStokAkhir() void
                        +getStokAkhir() int
                    }

                    EntitasGudang &lt;|-- Barang
                    Transaksi &lt;|-- BarangMasuk
                    Transaksi &lt;|-- BarangKeluar
                    Gudang *-- Barang : memiliki
                    Gudang *-- Transaksi : mencatat
                    Gudang *-- StokBarang : memantau
                    StokBarang --&gt; Barang : memantau
                    BarangMasuk --&gt; Barang : mengelola
                    BarangKeluar --&gt; Barang : mengelola
                </div>
            </div>

            <div class="copy-section">
                <button class="copy-btn" onclick="toggleCode('classdiagram-code')">Tampilkan Kode Mermaid</button>
                <button class="copy-btn" onclick="copyMermaid('classdiagram-code')">Salin Kode</button>
            </div>
            <div id="classdiagram-code" class="code-block">
                <span class="label">Kode Mermaid - Class Diagram</span>
                <code>classDiagram
                direction TB

                class EntitasGudang {
                    &lt;&lt;abstract&gt;&gt;
                    -String kode
                    -String nama
                    +EntitasGudang(kode nama)
                    +tampilkanInfo() void
                    +cetakIdentitas() void
                }

                class Barang {
                    -String kategori
                    -String merk
                    -int jumlahStok
                    -String satuan
                    -String kondisi
                    +Barang(kode nama kategori merk stok satuan kondisi)
                    +tampilkanInfo() void
                    +tambahStok(jumlah) bool
                    +kurangiStok(jumlah) bool
                    +getStok() int
                }

                class Gudang {
                    -List~Barang~ daftarBarang
                    -List~Transaksi~ riwayatTransaksi
                    -Map~StringStokBarang~ stokBarang
                    +Gudang()
                    +tambahBarang(barang) void
                    +cariBarang(kode) Barang
                    +tambahStok(kode jumlah) bool
                    +kurangiStok(kode jumlah) bool
                    +tampilkanSemuaBarang() void
                    +getTotalBarang() int
                    +init() void
                    +simulasiTransaksi() void
                }

                class Transaksi {
                    &lt;&lt;abstract&gt;&gt;
                    -String idTransaksi
                    -String tanggal
                    -String kodeBarang
                    -int jumlah
                    +Transaksi(id tanggal kode jumlah)
                    +prosesTransaksi() void
                    +cetakHeader() void
                }

                class BarangMasuk {
                    -String namaSupplier
                    +BarangMasuk(id tanggal kode jumlah supplier)
                    +prosesTransaksi() void
                }

                class BarangKeluar {
                    -String tujuan
                    +BarangKeluar(id tanggal kode jumlah tujuan)
                    +prosesTransaksi() void
                }

                class StokBarang {
                    -int stokAwal
                    -int barangMasuk
                    -int barangKeluar
                    -int stokAkhir
                    -String status
                    +StokBarang(stokAwal)
                    +tambahMasuk(jumlah) void
                    +tambahKeluar(jumlah) void
                    +hitungStokAkhir() void
                    +getStokAkhir() int
                }

                EntitasGudang &lt;|-- Barang
                Transaksi &lt;|-- BarangMasuk
                Transaksi &lt;|-- BarangKeluar
                Gudang *-- Barang : memiliki
                Gudang *-- Transaksi : mencatat
                Gudang *-- StokBarang : memantau
                StokBarang --&gt; Barang : memantau
                BarangMasuk --&gt; Barang : mengelola
                BarangKeluar --&gt; Barang : mengelola</code>
            </div>

            <!-- DIAGRAM 2: FLOWCHART ALUR TAMBAH STOK -->
            <h3 style="color:#34d399; margin-top:24px;">FLOWCHART ALUR TAMBAH STOK (BARANG MASUK)</h3>
            <p style="color:#94a3b8; font-size:0.85em; margin-bottom:6px;">
                Menunjukkan alur validasi saat melakukan penambahan stok barang (barang masuk ke gudang).
            </p>

            <div class="mermaid-wrapper">
                <div class="mermaid">
                    graph TD
                    A["START"] --> B["Input: kodeBarang, jumlah"]
                    B --> C["Cari Barang di Daftar"]
                    C --> D{"Barang ditemukan?"}
                    D -->|"Tidak"| E["Output: Error - Barang tidak ditemukan"]
                    E --> F["END - GAGAL"]

                    D -->|"Ya"| G{"Jumlah > 0?"}
                    G -->|"Tidak"| H["Output: Error - Jumlah harus lebih dari 0"]
                    H --> F

                    G -->|"Ya"| I["barang.tambahStok(jumlah)"]
                    I --> J["Update stokBarang"]
                    J --> K["Catat Riwayat Transaksi"]
                    K --> L["Output: Sukses - Stok bertambah"]
                    L --> M["END - SUKSES"]
                </div>
            </div>

            <div class="copy-section">
                <button class="copy-btn" onclick="toggleCode('tambahstok-code')">Tampilkan Kode Mermaid</button>
                <button class="copy-btn" onclick="copyMermaid('tambahstok-code')">Salin Kode</button>
            </div>
            <div id="tambahstok-code" class="code-block">
                <span class="label">Kode Mermaid - Alur Tambah Stok</span>
                <code>graph TD
                A["START"] --> B["Input: kodeBarang, jumlah"]
                B --> C["Cari Barang di Daftar"]
                C --> D{"Barang ditemukan?"}
                D -->|"Tidak"| E["Output: Error - Barang tidak ditemukan"]
                E --> F["END - GAGAL"]

                D -->|"Ya"| G{"Jumlah > 0?"}
                G -->|"Tidak"| H["Output: Error - Jumlah harus lebih dari 0"]
                H --> F

                G -->|"Ya"| I["barang.tambahStok(jumlah)"]
                I --> J["Update stokBarang"]
                J --> K["Catat Riwayat Transaksi"]
                K --> L["Output: Sukses - Stok bertambah"]
                L --> M["END - SUKSES"]</code>
            </div>

            <!-- DIAGRAM 3: FLOWCHART ALUR KURANGI STOK -->
            <h3 style="color:#f87171; margin-top:24px;">FLOWCHART ALUR KURANGI STOK (BARANG KELUAR)</h3>
            <p style="color:#94a3b8; font-size:0.85em; margin-bottom:6px;">
                Menunjukkan alur validasi saat melakukan pengurangan stok barang (barang keluar dari gudang).
            </p>

            <div class="mermaid-wrapper">
                <div class="mermaid">
                    graph TD
                    A["START"] --> B["Input: kodeBarang, jumlah"]
                    B --> C["Cari Barang di Daftar"]
                    C --> D{"Barang ditemukan?"}
                    D -->|"Tidak"| E["Output: Error - Barang tidak ditemukan"]
                    E --> F["END - GAGAL"]

                    D -->|"Ya"| G{"Jumlah > 0?"}
                    G -->|"Tidak"| H["Output: Error - Jumlah harus lebih dari 0"]
                    H --> F

                    G -->|"Ya"| I{"Stok >= jumlah?"}
                    I -->|"Tidak"| J["Output: Error - Stok tidak cukup"]
                    J --> F

                    I -->|"Ya"| K["barang.kurangiStok(jumlah)"]
                    K --> L["Update stokBarang"]
                    L --> M["Catat Riwayat Transaksi"]
                    M --> N["Output: Sukses - Stok berkurang"]
                    N --> O["END - SUKSES"]
                </div>
            </div>

            <div class="copy-section">
                <button class="copy-btn" onclick="toggleCode('kurangistok-code')">Tampilkan Kode Mermaid</button>
                <button class="copy-btn" onclick="copyMermaid('kurangistok-code')">Salin Kode</button>
            </div>
            <div id="kurangistok-code" class="code-block">
                <span class="label">Kode Mermaid - Alur Kurangi Stok</span>
                <code>graph TD
                A["START"] --> B["Input: kodeBarang, jumlah"]
                B --> C["Cari Barang di Daftar"]
                C --> D{"Barang ditemukan?"}
                D -->|"Tidak"| E["Output: Error - Barang tidak ditemukan"]
                E --> F["END - GAGAL"]

                D -->|"Ya"| G{"Jumlah > 0?"}
                G -->|"Tidak"| H["Output: Error - Jumlah harus lebih dari 0"]
                H --> F

                G -->|"Ya"| I{"Stok >= jumlah?"}
                I -->|"Tidak"| J["Output: Error - Stok tidak cukup"]
                J --> F

                I -->|"Ya"| K["barang.kurangiStok(jumlah)"]
                K --> L["Update stokBarang"]
                L --> M["Catat Riwayat Transaksi"]
                M --> N["Output: Sukses - Stok berkurang"]
                N --> O["END - SUKSES"]</code>
            </div>

            <!-- PSEUDOCODE LENGKAP -->
            <div style="margin-top:20px; background:rgba(2,6,23,0.6); border-radius:8px; padding:16px; border-left:3px solid #fbbf24;">
                <h4 style="color:#fbbf24; font-size:0.9em;">PSEUDOCODE LENGKAP</h4>
                <div class="pseudocode-container">
                    <div class="pseudocode-box" style="border-left-color:#34d399;">
                        <h5 style="color:#34d399;">Tambah Stok</h5>
                        <pre><span class="keyword">ALGORITMA</span> TambahStok
    <span class="input">INPUT:</span> kode, jumlah
    
    <span class="keyword">IF</span> barang tidak ditemukan <span class="keyword">THEN</span>
        <span class="error">OUTPUT "Error - Barang tidak ditemukan"</span>
        <span class="keyword">RETURN</span> <span class="keyword">false</span>
    <span class="keyword">END IF</span>
    
    <span class="keyword">IF</span> jumlah <= 0 <span class="keyword">THEN</span>
        <span class="error">OUTPUT "Error - Jumlah harus lebih dari 0"</span>
        <span class="keyword">RETURN</span> <span class="keyword">false</span>
    <span class="keyword">END IF</span>
    
    barang.jumlahStok += jumlah
    catat riwayat transaksi
    <span class="output">OUTPUT "Sukses - Stok bertambah"</span>
    <span class="keyword">RETURN</span> <span class="keyword">true</span></pre>
                    </div>

                    <div class="pseudocode-box" style="border-left-color:#f87171;">
                        <h5 style="color:#f87171;">Kurangi Stok</h5>
                        <pre><span class="keyword">ALGORITMA</span> KurangiStok
    <span class="input">INPUT:</span> kode, jumlah
    
    <span class="keyword">IF</span> barang tidak ditemukan <span class="keyword">THEN</span>
        <span class="error">OUTPUT "Error - Barang tidak ditemukan"</span>
        <span class="keyword">RETURN</span> <span class="keyword">false</span>
    <span class="keyword">END IF</span>
    
    <span class="keyword">IF</span> jumlah <= 0 <span class="keyword">THEN</span>
        <span class="error">OUTPUT "Error - Jumlah harus lebih dari 0"</span>
        <span class="keyword">RETURN</span> <span class="keyword">false</span>
    <span class="keyword">END IF</span>
    
    <span class="keyword">IF</span> stok < jumlah <span class="keyword">THEN</span>
        <span class="error">OUTPUT "Error - Stok tidak cukup"</span>
        <span class="keyword">RETURN</span> <span class="keyword">false</span>
    <span class="keyword">END IF</span>
    
    barang.jumlahStok -= jumlah
    catat riwayat transaksi
    <span class="output">OUTPUT "Sukses - Stok berkurang"</span>
    <span class="keyword">RETURN</span> <span class="keyword">true</span></pre>
                    </div>
                </div>
            </div>
        </div>

        <!-- 4 PILAR OOP -->
        <div class="section" style="border:2px solid rgba(52,211,153,0.3);">
            <h2 style="color:#34d399 !important;">4 Pilar OOP - Implementasi</h2>
            <div class="grid-2">
                <div class="pillar-card">
                    <h4>1. Enkapsulasi (Encapsulation)</h4>
                    <p>Data stok (<b>jumlahStok</b>) disembunyikan dan hanya diubah melalui metode <b>tambahStok()</b> dan <b>kurangiStok()</b>. Properti private (-), method public (+).</p>
                </div>
                <div class="pillar-card">
                    <h4>2. Pewarisan (Inheritance)</h4>
                    <p><b>Barang</b> mewarisi <b>EntitasGudang</b>. <b>BarangMasuk</b> dan <b>BarangKeluar</b> mewarisi <b>Transaksi</b>. Menggunakan ulang kode.</p>
                </div>
                <div class="pillar-card">
                    <h4>3. Polimorfisme (Polymorphism)</h4>
                    <p>Metode <b>tampilkanInfo()</b> di-override di <b>Barang</b>. Metode <b>prosesTransaksi()</b> di-override di turunan <b>Transaksi</b>.</p>
                </div>
                <div class="pillar-card">
                    <h4>4. Interaksi Objek (Object Interaction)</h4>
                    <p><b>Gudang</b> berkomposisi dengan <b>Barang</b> dan <b>Transaksi</b>. <b>StokBarang</b> berinteraksi dengan <b>Barang</b> untuk memantau stok.</p>
                </div>
            </div>
        </div>

        <!-- SOURCE CODE -->
        <div class="section">
            <h2>Source Code - Sistem Pendataan Barang (Dart)</h2>
            <div class="source-code-container">
                <span class="comment">// ==========================================</span>
                <span class="comment">// Nama  : Yoza Ulpia Rafila dan Rifqi Prayoga</span>
                <span class="comment">// NIM   : 251410004 dan 251410005</span>
                <span class="comment">// Kelas : SI2A</span>
                <span class="comment">// Topik : Sistem Pendataan Barang di Gudang (OOP)</span>
                <span class="comment">// ==========================================</span>

                <span class="comment">// ABSTRACT CLASS</span>
                <span class="keyword">abstract class</span> <span class="class-name">EntitasGudang</span> {
                    <span class="variable">String</span> kode, nama;
                    <span class="class-name">EntitasGudang</span>(<span class="keyword">this</span>.kode, <span class="keyword">this</span>.nama);
                    <span class="method">void tampilkanInfo</span>();
                    <span class="method">void cetakIdentitas</span>() {
                        <span class="function">print</span>(<span class="string">"$kode -- $nama"</span>);
                    }
                }

                <span class="comment">// BARANG CLASS (INHERITANCE)</span>
                <span class="keyword">class</span> <span class="class-name">Barang</span> <span class="keyword">extends</span> <span class="class-name">EntitasGudang</span> {
                    <span class="variable">String</span> kategori, merk, satuan, kondisi;
                    <span class="variable">int</span> jumlahStok;

                    <span class="class-name">Barang</span>(
                        <span class="variable">String</span> kode, 
                        <span class="variable">String</span> nama, 
                        <span class="keyword">this</span>.kategori, 
                        <span class="keyword">this</span>.merk,
                        <span class="keyword">this</span>.jumlahStok, 
                        <span class="keyword">this</span>.satuan, 
                        <span class="keyword">this</span>.kondisi
                    ) : <span class="keyword">super</span>(kode, nama);

                    <span class="annotation">@override</span>
                    <span class="method">void tampilkanInfo</span>() {
                        <span class="function">print</span>(
                            <span class="string">"$kode | $nama | $kategori | Stok: $jumlahStok $satuan | $kondisi"</span>
                        );
                    }

                    <span class="comment">// ALGORITMA TAMBAH STOK</span>
                    <span class="type">bool</span> <span class="method">tambahStok</span>(<span class="variable">int</span> jumlah) {
                        <span class="keyword">if</span> (jumlah > <span class="number">0</span>) {
                            jumlahStok += jumlah;
                            <span class="function">print</span>(<span class="string">"Stok $nama +$jumlah. Total: $jumlahStok $satuan"</span>);
                            <span class="keyword">return</span> <span class="keyword">true</span>;
                        }
                        <span class="function">print</span>(<span class="string">"Jumlah harus > 0!"</span>);
                        <span class="keyword">return</span> <span class="keyword">false</span>;
                    }

                    <span class="comment">// ALGORITMA KURANGI STOK</span>
                    <span class="type">bool</span> <span class="method">kurangiStok</span>(<span class="variable">int</span> jumlah) {
                        <span class="keyword">if</span> (jumlah <= <span class="number">0</span>) {
                            <span class="function">print</span>(<span class="string">"Jumlah harus > 0!"</span>);
                            <span class="keyword">return</span> <span class="keyword">false</span>;
                        }
                        <span class="keyword">if</span> (jumlahStok >= jumlah) {
                            jumlahStok -= jumlah;
                            <span class="function">print</span>(<span class="string">"Stok $nama -$jumlah. Total: $jumlahStok $satuan"</span>);
                            <span class="keyword">return</span> <span class="keyword">true</span>;
                        }
                        <span class="function">print</span>(<span class="string">"Stok tidak cukup! Tersisa: $jumlahStok $satuan"</span>);
                        <span class="keyword">return</span> <span class="keyword">false</span>;
                    }

                    <span class="type">int</span> <span class="method">getStok</span>() => jumlahStok;
                }

                <span class="comment">// ABSTRACT TRANSACTION</span>
                <span class="keyword">abstract class</span> <span class="class-name">Transaksi</span> {
                    <span class="variable">String</span> idTransaksi, tanggal, kodeBarang;
                    <span class="variable">int</span> jumlah;
                    <span class="class-name">Transaksi</span>(
                        <span class="keyword">this</span>.idTransaksi, 
                        <span class="keyword">this</span>.tanggal, 
                        <span class="keyword">this</span>.kodeBarang, 
                        <span class="keyword">this</span>.jumlah
                    );
                    <span class="method">void prosesTransaksi</span>();
                    <span class="method">void cetakHeader</span>() {
                        <span class="function">print</span>(<span class="string">"ID: $idTransaksi | Tanggal: $tanggal | Kode: $kodeBarang"</span>);
                    }
                }

                <span class="comment">// BARANG MASUK (INHERITANCE)</span>
                <span class="keyword">class</span> <span class="class-name">BarangMasuk</span> <span class="keyword">extends</span> <span class="class-name">Transaksi</span> {
                    <span class="variable">String</span> namaSupplier;
                    <span class="class-name">BarangMasuk</span>(
                        <span class="variable">String</span> id, 
                        <span class="variable">String</span> tanggal, 
                        <span class="variable">String</span> kode, 
                        <span class="variable">int</span> jumlah, 
                        <span class="keyword">this</span>.namaSupplier
                    ) : <span class="keyword">super</span>(id, tanggal, kode, jumlah);
                    
                    <span class="annotation">@override</span>
                    <span class="method">void prosesTransaksi</span>() {
                        <span class="function">print</span>(<span class="string">"Barang masuk dari $namaSupplier sebanyak $jumlah"</span>);
                    }
                }

                <span class="comment">// BARANG KELUAR (INHERITANCE)</span>
                <span class="keyword">class</span> <span class="class-name">BarangKeluar</span> <span class="keyword">extends</span> <span class="class-name">Transaksi</span> {
                    <span class="variable">String</span> tujuan;
                    <span class="class-name">BarangKeluar</span>(
                        <span class="variable">String</span> id, 
                        <span class="variable">String</span> tanggal, 
                        <span class="variable">String</span> kode, 
                        <span class="variable">int</span> jumlah, 
                        <span class="keyword">this</span>.tujuan
                    ) : <span class="keyword">super</span>(id, tanggal, kode, jumlah);
                    
                    <span class="annotation">@override</span>
                    <span class="method">void prosesTransaksi</span>() {
                        <span class="function">print</span>(<span class="string">"Barang keluar ke $tujuan sebanyak $jumlah"</span>);
                    }
                }

                <span class="comment">// STOK BARANG (COMPOSITION)</span>
                <span class="keyword">class</span> <span class="class-name">StokBarang</span> {
                    <span class="variable">int</span> stokAwal, barangMasuk, barangKeluar, stokAkhir;
                    <span class="variable">String</span> status;
                    
                    <span class="class-name">StokBarang</span>(<span class="keyword">this</span>.stokAwal)
                        : barangMasuk = <span class="number">0</span>, 
                          barangKeluar = <span class="number">0</span>, 
                          stokAkhir = stokAwal, 
                          status = <span class="string">"Stabil"</span>;

                    <span class="method">void tambahMasuk</span>(<span class="variable">int</span> jumlah) { 
                        barangMasuk += jumlah; 
                        <span class="method">hitungStokAkhir</span>(); 
                    }
                    
                    <span class="method">void tambahKeluar</span>(<span class="variable">int</span> jumlah) { 
                        barangKeluar += jumlah; 
                        <span class="method">hitungStokAkhir</span>(); 
                    }
                    
                    <span class="method">void hitungStokAkhir</span>() {
                        stokAkhir = stokAwal + barangMasuk - barangKeluar;
                        <span class="keyword">if</span> (stokAkhir < <span class="number">5</span>) status = <span class="string">"Stok Menipis!"</span>;
                        <span class="keyword">else if</span> (stokAkhir > <span class="number">50</span>) status = <span class="string">"Stok Berlebih"</span>;
                        <span class="keyword">else</span> status = <span class="string">"Stabil"</span>;
                    }
                    
                    <span class="type">int</span> <span class="method">getStokAkhir</span>() => stokAkhir;
                }

                <span class="comment">// GUDANG (COMPOSITION & INTERACTION)</span>
                <span class="keyword">class</span> <span class="class-name">Gudang</span> {
                    <span class="type">List&lt;Barang&gt;</span> daftarBarang = [];
                    <span class="type">List&lt;Transaksi&gt;</span> riwayatTransaksi = [];
                    <span class="type">Map&lt;String, StokBarang&gt;</span> stokBarang = {};

                    <span class="method">void tambahBarang</span>(<span class="type">Barang</span> b) {
                        <span class="keyword">if</span> (<span class="method">cariBarang</span>(b.kode) != <span class="keyword">null</span>) {
                            <span class="function">print</span>(<span class="string">"Kode ${b.kode} sudah ada!"</span>);
                            <span class="keyword">return</span>;
                        }
                        daftarBarang.<span class="method">add</span>(b);
                        stokBarang[b.kode] = <span class="class-name">StokBarang</span>(b.jumlahStok);
                        <span class="function">print</span>(<span class="string">"${b.nama} berhasil ditambahkan!"</span>);
                    }

                    <span class="type">Barang?</span> <span class="method">cariBarang</span>(<span class="variable">String</span> kode) {
                        <span class="keyword">try</span> {
                            <span class="keyword">return</span> daftarBarang.<span class="method">firstWhere</span>((b) => b.kode == kode);
                        } <span class="keyword">catch</span> (e) {
                            <span class="keyword">return</span> <span class="keyword">null</span>;
                        }
                    }

                    <span class="comment">// IMPLEMENTASI ALGORITMA TAMBAH STOK</span>
                    <span class="type">bool</span> <span class="method">tambahStok</span>(<span class="variable">String</span> kode, <span class="variable">int</span> jumlah) {
                        <span class="type">Barang?</span> b = <span class="method">cariBarang</span>(kode);
                        <span class="keyword">if</span> (b == <span class="keyword">null</span>) { 
                            <span class="function">print</span>(<span class="string">"Barang tidak ditemukan!"</span>); 
                            <span class="keyword">return</span> <span class="keyword">false</span>; 
                        }
                        
                        <span class="type">bool</span> hasil = b.<span class="method">tambahStok</span>(jumlah);
                        <span class="keyword">if</span> (hasil && stokBarang.<span class="method">containsKey</span>(kode)) {
                            stokBarang[kode]!.<span class="method">tambahMasuk</span>(jumlah);
                            riwayatTransaksi.<span class="method">add</span>(
                                <span class="class-name">BarangMasuk</span>(
                                    <span class="string">"TRX-${DateTime.now().millisecondsSinceEpoch}"</span>,
                                    <span class="class-name">DateTime</span>.<span class="method">now</span>().<span class="method">toString</span>(), 
                                    kode, jumlah, <span class="string">"Sistem"</span>
                                )
                            );
                        }
                        <span class="keyword">return</span> hasil;
                    }

                    <span class="comment">// IMPLEMENTASI ALGORITMA KURANGI STOK</span>
                    <span class="type">bool</span> <span class="method">kurangiStok</span>(<span class="variable">String</span> kode, <span class="variable">int</span> jumlah) {
                        <span class="type">Barang?</span> b = <span class="method">cariBarang</span>(kode);
                        <span class="keyword">if</span> (b == <span class="keyword">null</span>) { 
                            <span class="function">print</span>(<span class="string">"Barang tidak ditemukan!"</span>); 
                            <span class="keyword">return</span> <span class="keyword">false</span>; 
                        }
                        
                        <span class="type">bool</span> hasil = b.<span class="method">kurangiStok</span>(jumlah);
                        <span class="keyword">if</span> (hasil && stokBarang.<span class="method">containsKey</span>(kode)) {
                            stokBarang[kode]!.<span class="method">tambahKeluar</span>(jumlah);
                            riwayatTransaksi.<span class="method">add</span>(
                                <span class="class-name">BarangKeluar</span>(
                                    <span class="string">"TRX-${DateTime.now().millisecondsSinceEpoch}"</span>,
                                    <span class="class-name">DateTime</span>.<span class="method">now</span>().<span class="method">toString</span>(), 
                                    kode, jumlah, <span class="string">"Pelanggan"</span>
                                )
                            );
                        }
                        <span class="keyword">return</span> hasil;
                    }

                    <span class="method">void tampilkanSemuaBarang</span>() {
                        <span class="function">print</span>(<span class="string">"\nDAFTAR BARANG"</span>);
                        <span class="keyword">if</span> (daftarBarang.<span class="method">isEmpty</span>) { 
                            <span class="function">print</span>(<span class="string">"Belum ada barang."</span>); 
                            <span class="keyword">return</span>; 
                        }
                        <span class="keyword">for</span> (<span class="keyword">var</span> b <span class="keyword">in</span> daftarBarang) {
                            b.<span class="method">tampilkanInfo</span>();
                            <span class="keyword">if</span> (stokBarang.<span class="method">containsKey</span>(b.kode)) {
                                <span class="function">print</span>(<span class="string">"   Status: ${stokBarang[b.kode]!.status}"</span>);
                            }
                        }
                        <span class="function">print</span>(<span class="string">"Total: ${daftarBarang.length} barang\n"</span>);
                    }

                    <span class="method">void init</span>() {
                        <span class="method">tambahBarang</span>(
                            <span class="class-name">Barang</span>(<span class="string">"BRG001"</span>, <span class="string">"Beras Premium"</span>, <span class="string">"Makanan"</span>, <span class="string">"A"</span>, <span class="number">50</span>, <span class="string">"Karung"</span>, <span class="string">"Baik"</span>)
                        );
                        <span class="method">tambahBarang</span>(
                            <span class="class-name">Barang</span>(<span class="string">"BRG002"</span>, <span class="string">"Gula Pasir"</span>, <span class="string">"Pokok"</span>, <span class="string">"B"</span>, <span class="number">40</span>, <span class="string">"Kg"</span>, <span class="string">"Baik"</span>)
                        );
                        <span class="method">tambahBarang</span>(
                            <span class="class-name">Barang</span>(<span class="string">"BRG003"</span>, <span class="string">"Minyak Goreng"</span>, <span class="string">"Pokok"</span>, <span class="string">"C"</span>, <span class="number">35</span>, <span class="string">"Liter"</span>, <span class="string">"Baik"</span>)
                        );
                        <span class="method">tambahBarang</span>(
                            <span class="class-name">Barang</span>(<span class="string">"BRG004"</span>, <span class="string">"Telur Ayam"</span>, <span class="string">"Makanan"</span>, <span class="string">"D"</span>, <span class="number">30</span>, <span class="string">"Kg"</span>, <span class="string">"Baik"</span>)
                        );
                        <span class="method">tambahBarang</span>(
                            <span class="class-name">Barang</span>(<span class="string">"BRG005"</span>, <span class="string">"Tepung Terigu"</span>, <span class="string">"Pokok"</span>, <span class="string">"E"</span>, <span class="number">45</span>, <span class="string">"Kg"</span>, <span class="string">"Baik"</span>)
                        );
                        <span class="function">print</span>(<span class="string">"\nData siap! ${daftarBarang.length} barang.\n"</span>);
                    }

                    <span class="method">void simulasiTransaksi</span>() {
                        <span class="function">print</span>(<span class="string">"\n>>> SIMULASI TRANSAKSI <<<"</span>);
                        <span class="method">tambahStok</span>(<span class="string">"BRG001"</span>, <span class="number">20</span>);
                        <span class="method">kurangiStok</span>(<span class="string">"BRG002"</span>, <span class="number">10</span>);
                        <span class="method">tambahStok</span>(<span class="string">"BRG003"</span>, <span class="number">15</span>);
                        <span class="method">kurangiStok</span>(<span class="string">"BRG004"</span>, <span class="number">40</span>); <span class="comment">// Gagal</span>
                        <span class="method">tambahStok</span>(<span class="string">"BRG005"</span>, <span class="number">10</span>);
                        <span class="method">kurangiStok</span>(<span class="string">"BRG001"</span>, <span class="number">15</span>);
                        <span class="method">tambahBarang</span>(
                            <span class="class-name">Barang</span>(<span class="string">"BRG006"</span>, <span class="string">"Mie Instan"</span>, <span class="string">"Instan"</span>, <span class="string">"F"</span>, <span class="number">50</span>, <span class="string">"Kg"</span>, <span class="string">"Baik"</span>)
                        );
                        <span class="method">kurangiStok</span>(<span class="string">"BRG003"</span>, <span class="number">5</span>);
                        <span class="method">kurangiStok</span>(<span class="string">"BRG999"</span>, <span class="number">10</span>); <span class="comment">// Gagal</span>
                        <span class="method">tambahStok</span>(<span class="string">"BRG004"</span>, <span class="number">20</span>);
                        <span class="function">print</span>(<span class="string">">>> SIMULASI SELESAI <<<\n"</span>);
                        <span class="method">tampilkanSemuaBarang</span>();
                    }
                }

                <span class="comment">// MAIN FUNCTION</span>
                <span class="method">void main</span>() {
                    <span class="keyword">var</span> gudang = <span class="class-name">Gudang</span>();
                    gudang.<span class="method">init</span>();
                    gudang.<span class="method">simulasiTransaksi</span>(); <span class="comment">// Langsung jalankan simulasi tanpa input pengguna</span>
                }
            </div>

            <div class="dartpad-row">
                <button class="btn" onclick="runDart('d1','https://dartpad.dev/embed-inline.html?id=526a8fea48af9282cae0ce70c84dc079&split=60&run=true')">Tampilkan DartPad</button>
            </div>
            <iframe id="d1" width="100%" height="500" style="border:1px solid #ccc; border-radius:8px; display:none;"></iframe>

            <div class="spacer"></div>
        </div>

        <!-- FOOTER -->
        <footer>
            <strong>Sistem Pendataan Barang di Gudang</strong> - Penerapan OOP berbasis Dart<br />
            Universitas Bina Darma - SI2A - 2026<br />
            <span style="color:#64748b;">Yoza Ulpia Rafila (251410004) &amp; Rifqi Prayoga (251410005)</span>
        </footer>

    </div>

    <!-- JAVASCRIPT -->
    <script>
        // DATA
        let barangList = [];
        const initialData = [
            { kode: 'BRG-001', nama: 'Laptop Asus', kategori: 'Elektronik', merk: 'Asus', stok: 10, satuan: 'unit',
                kondisi: 'Baik' },
            { kode: 'BRG-002', nama: 'Printer Epson', kategori: 'Elektronik', merk: 'Epson', stok: 5, satuan: 'unit',
                kondisi: 'Baik' },
            { kode: 'BRG-003', nama: 'Meja Kerja', kategori: 'Furniture', merk: 'IKEA', stok: 8, satuan: 'pcs',
                kondisi: 'Baik' },
            { kode: 'BRG-004', nama: 'Kursi Kantor', kategori: 'Furniture', merk: 'IKEA', stok: 12, satuan: 'pcs',
                kondisi: 'Baik' },
            { kode: 'BRG-005', nama: 'Kertas A4', kategori: 'ATK', merk: 'PaperOne', stok: 50, satuan: 'rim',
                kondisi: 'Baik' },
        ];

        // CLASSES (JS)
        class EntitasGudang {
            constructor(kode, nama) { this.kode = kode;
                this.nama = nama; }
            tampilkanInfo() { throw new Error('abstract'); }
        }

        class Barang extends EntitasGudang {
            constructor(kode, nama, kategori, merk, stok, satuan, kondisi) {
                super(kode, nama);
                this.kategori = kategori;
                this.merk = merk;
                this.jumlahStok = stok;
                this.satuan = satuan;
                this.kondisi = kondisi;
            }
            tampilkanInfo() {
                return this.kode + ' | ' + this.nama + ' | ' + this.kategori + ' | Stok: ' + this.jumlahStok + ' ' + this
                    .satuan + ' | ' + this.kondisi;
            }
            tambahStok(j) {
                if (j > 0) { this.jumlahStok += j;
                    log('Stok ' + this.nama + ' +' + j + '. Total: ' + this.jumlahStok, 'green'); return true; }
                return false;
            }
            kurangiStok(j) {
                if (j <= 0) return false;
                if (this.jumlahStok >= j) { this.jumlahStok -= j;
                    log('Stok ' + this.nama + ' -' + j + '. Total: ' + this.jumlahStok, 'green'); return true; }
                log('Stok ' + this.nama + ' tidak cukup!', 'red');
                return false;
            }
        }

        // TERMINAL
        function log(msg, cls = '') {
            const t = document.getElementById('terminal');
            if (!t) return;
            const d = document.createElement('div');
            d.className = 'log-line';
            d.innerHTML = '<span class="time">[' + new Date().toLocaleTimeString() + ']</span> <span class="' + cls + '">' + msg +
                '</span>';
            t.appendChild(d);
            t.scrollTop = t.scrollHeight;
        }

        function clearTerminal() {
            const t = document.getElementById('terminal');
            if (t) t.innerHTML = '';
            log('Terminal dibersihkan.', 'gray');
        }

        // SELECT / UI
        function refreshSelect() {
            const sel = document.getElementById('selectBarang');
            if (!sel) return;
            sel.innerHTML = '';
            if (!barangList.length) { sel.innerHTML = '<option value="">- tidak ada -</option>'; return; }
            barangList.forEach(function(b) {
                const o = document.createElement('option');
                o.value = b.kode;
                o.text = b.kode + ' - ' + b.nama + ' (' + b.jumlahStok + ')';
                sel.appendChild(o);
            });
            sel.value = barangList[0].kode;
            onSelectChange();
        }

        function onSelectChange() {
            const sel = document.getElementById('selectBarang');
            const info = document.getElementById('infoBarang');
            if (!sel || !info) return;
            const b = barangList.find(function(x) { return x.kode === sel.value; });
            info.textContent = b ? b.nama + ' | Stok: ' + b.jumlahStok + ' ' + b.satuan : 'Tidak ada barang';
        }

        function getSelected() {
            const sel = document.getElementById('selectBarang');
            if (!sel) return null;
            return barangList.find(function(x) { return x.kode === sel.value; }) || null;
        }

        // CRUD
        function tambahBarang() {
            const kode = document.getElementById('newKode').value.trim();
            const nama = document.getElementById('newNama').value.trim();
            const kategori = document.getElementById('newKategori').value.trim();
            const stok = parseInt(document.getElementById('newStok').value) || 0;
            if (!kode || !nama || !kategori) { log('Semua field harus diisi!', 'red'); return; }
            if (barangList.some(function(b) { return b.kode === kode; })) { log('Kode "' + kode + '" sudah ada!', 'red'); return; }
            const b = new Barang(kode, nama, kategori, '-', stok, 'unit', 'Baik');
            barangList.push(b);
            log('"' + nama + '" (' + kode + ') ditambahkan.', 'green');
            refreshSelect();
            renderInventory();
            document.getElementById('newKode').value = 'BRG-' + String(barangList.length + 1).padStart(3, '0');
            document.getElementById('newNama').value = '';
            document.getElementById('newKategori').value = '';
            document.getElementById('newStok').value = '0';
        }

        function tambahStok() {
            const b = getSelected();
            if (!b) return;
            const j = parseInt(prompt('Jumlah tambah:', '1'));
            if (j > 0 && b.tambahStok(j)) { renderInventory();
                refreshSelect(); }
        }

        function kurangiStok() {
            const b = getSelected();
            if (!b) return;
            const j = parseInt(prompt('Jumlah kurangi:', '1'));
            if (j > 0 && b.kurangiStok(j)) { renderInventory();
                refreshSelect(); }
        }

        function tampilkanBarang() {
            const b = getSelected();
            if (b) log(b.tampilkanInfo(), 'cyan');
        }

        function hapusBarang() {
            const b = getSelected();
            if (!b) return;
            if (!confirm('Hapus "' + b.nama + '"?')) return;
            barangList = barangList.filter(function(x) { return x.kode !== b.kode; });
            log('"' + b.nama + '" dihapus.', 'red');
            refreshSelect();
            renderInventory();
        }

        // SIMULASI
        function simulasiTransaksi() {
            log('Memulai simulasi 10 transaksi...', 'purple');
            log('-----------------------------------------', 'gray');
            setTimeout(function() {
                const b1 = barangList.find(function(b) { return b.kode === 'BRG-001'; });
                if (b1) { log('Transaksi 1: ' + b1.nama + ' +20', 'cyan');
                    b1.tambahStok(20);
                    renderInventory();
                    refreshSelect(); }
            }, 300);
            setTimeout(function() {
                const b2 = barangList.find(function(b) { return b.kode === 'BRG-002'; });
                if (b2) { log('Transaksi 2: ' + b2.nama + ' -10', 'cyan');
                    b2.kurangiStok(10);
                    renderInventory();
                    refreshSelect(); }
            }, 800);
            setTimeout(function() {
                const b3 = barangList.find(function(b) { return b.kode === 'BRG-003'; });
                if (b3) { log('Transaksi 3: ' + b3.nama + ' +15', 'cyan');
                    b3.tambahStok(15);
                    renderInventory();
                    refreshSelect(); }
            }, 1300);
            setTimeout(function() {
                const b4 = barangList.find(function(b) { return b.kode === 'BRG-004'; });
                if (b4) { log('Transaksi 4: ' + b4.nama + ' -40 (Gagal)', 'yellow');
                    b4.kurangiStok(40);
                    renderInventory();
                    refreshSelect(); }
            }, 1800);
            setTimeout(function() {
                const b5 = barangList.find(function(b) { return b.kode === 'BRG-005'; });
                if (b5) { log('Transaksi 5: ' + b5.nama + ' +10', 'cyan');
                    b5.tambahStok(10);
                    renderInventory();
                    refreshSelect(); }
            }, 2300);
            setTimeout(function() {
                const b1 = barangList.find(function(b) { return b.kode === 'BRG-001'; });
                if (b1) { log('Transaksi 6: ' + b1.nama + ' -15', 'cyan');
                    b1.kurangiStok(15);
                    renderInventory();
                    refreshSelect(); }
            }, 2800);
            setTimeout(function() {
                log('Transaksi 7: Mie Instan +50 (Barang Baru)', 'cyan');
                const b = new Barang('BRG-006', 'Mie Instan', 'Instan', '-', 50, 'Kg', 'Baik');
                barangList.push(b);
                log('"Mie Instan" ditambahkan.', 'green');
                renderInventory();
                refreshSelect();
            }, 3300);
            setTimeout(function() {
                const b3 = barangList.find(function(b) { return b.kode === 'BRG-003'; });
                if (b3) { log('Transaksi 8: ' + b3.nama + ' -5', 'cyan');
                    b3.kurangiStok(5);
                    renderInventory();
                    refreshSelect(); }
            }, 3800);
            setTimeout(function() {
                log('Transaksi 9: BRG999 -10 (Gagal)', 'yellow');
                const b = barangList.find(function(b) { return b.kode === 'BRG999'; });
                if (!b) log('Barang tidak ditemukan!', 'red');
            }, 4300);
            setTimeout(function() {
                const b4 = barangList.find(function(b) { return b.kode === 'BRG-004'; });
                if (b4) { log('Transaksi 10: ' + b4.nama + ' +20', 'cyan');
                    b4.tambahStok(20);
                    renderInventory();
                    refreshSelect(); }
            }, 4800);
            setTimeout(function() {
                log('-----------------------------------------', 'gray');
                log('Simulasi selesai! Total barang: ' + barangList.length, 'purple');
            }, 5300);
        }

        // RENDER
        function renderInventory() {
            const g = document.getElementById('inventoryGrid');
            if (!g) return;
            g.innerHTML = '';
            if (!barangList.length) { g.innerHTML =
                    '<p style="color:#94a3b8;text-align:center;grid-column:1/-1;">Belum ada barang.</p>'; return; }
            barangList.forEach(function(b) {
                const c = document.createElement('div');
                c.className = 'card';
                const statusClass = b.jumlahStok > 0 ? 'available' : 'rented';
                const statusText = b.jumlahStok > 0 ? 'Tersedia' : 'Habis';
                c.innerHTML = '<div class="card-title">' + b.nama + '</div>' +
                    '<div class="card-sub">' + b.kode + ' · ' + b.kategori + '</div>' +
                    '<div class="card-sub">Stok: <b>' + b.jumlahStok + '</b> ' + b.satuan + '</div>' +
                    '<div style="margin-top:6px;"><span class="badge ' + statusClass + '">' + statusText + '</span></div>' +
                    '<div style="margin-top:10px; display:flex; gap:6px; flex-wrap:wrap;">' +
                    '<button class="btn green small" onclick="quickAdd(\'' + b.kode + '\')">+ Tambah</button>' +
                    '<button class="btn orange small" onclick="quickSub(\'' + b.kode + '\')">- Kurang</button>' +
                    '<button class="btn purple small" onclick="quickDetail(\'' + b.kode + '\')">Detail</button>' +
                    '</div>';
                g.appendChild(c);
            });
        }

        function quickAdd(k) { const b = barangList.find(function(x) { return x.kode === k; }); if (!b) return; const j = parseInt(
                prompt('Tambah:', '1')); if (j > 0 && b.tambahStok(j)) { renderInventory();
                refreshSelect(); } }

        function quickSub(k) { const b = barangList.find(function(x) { return x.kode === k; }); if (!b) return; const j = parseInt(
                prompt('Kurangi:', '1')); if (j > 0 && b.kurangiStok(j)) { renderInventory();
                refreshSelect(); } }

        function quickDetail(k) { const b = barangList.find(function(x) { return x.kode === k; }); if (b) log(b.tampilkanInfo(),
                'cyan'); }

        // MERMAID INIT
        mermaid.initialize({
            startOnLoad: true,
            theme: 'dark',
            securityLevel: 'loose',
            themeVariables: {
                primaryColor: '#38bdf8',
                primaryTextColor: '#fff',
                primaryBorderColor: '#818cf8',
                lineColor: '#94a3b8',
                secondaryColor: '#1e293b',
                tertiaryColor: '#0f172a',
                background: '#020617',
                fontFamily: 'Segoe UI, sans-serif',
                fontSize: '14px'
            },
            flowchart: { htmlLabels: true, curve: 'basis', useMaxWidth: true }
        });

        // FUNCTIONS FOR CODE BLOCKS
        function toggleCode(id) {
            const el = document.getElementById(id);
            if (el) {
                el.classList.toggle('show');
                const btn = el.parentElement.querySelector('.copy-btn:first-child');
                if (btn) {
                    btn.textContent = el.classList.contains('show') ? 'Sembunyikan Kode' : 'Tampilkan Kode Mermaid';
                }
            }
        }

        function copyMermaid(id) {
            const el = document.getElementById(id);
            if (!el) return;
            const code = el.querySelector('code');
            if (!code) return;
            const text = code.textContent;
            if (!el.classList.contains('show')) {
                el.classList.add('show');
                const btn = el.parentElement.querySelector('.copy-btn:first-child');
                if (btn) btn.textContent = 'Sembunyikan Kode';
            }
            navigator.clipboard.writeText(text).then(function() {
                const btns = el.parentElement.querySelectorAll('.copy-btn');
                btns.forEach(function(btn) {
                    if (btn.textContent.includes('Salin')) {
                        const orig = btn.textContent;
                        btn.textContent = 'Disalin!';
                        btn.classList.add('active');
                        setTimeout(function() {
                            btn.textContent = orig;
                            btn.classList.remove('active');
                        }, 2000);
                    }
                });
            }).catch(function(err) {
                alert('Gagal menyalin: ' + err);
                const range = document.createRange();
                range.selectNode(code);
                window.getSelection().removeAllRanges();
                window.getSelection().addRange(range);
                document.execCommand('copy');
            });
        }

        // DARTPAD
        function runDart(id, url) {
            let iframe = document.getElementById(id);
            iframe.style.display = "block";
            iframe.src = url;
        }

        // INIT
        function init() {
            initialData.forEach(function(d) {
                barangList.push(new Barang(d.kode, d.nama, d.kategori, d.merk, d.stok, d.satuan, d.kondisi));
            });
            log(barangList.length + ' barang siap.', 'green');
            refreshSelect();
            renderInventory();
            const sel = document.getElementById('selectBarang');
            if (sel) sel.addEventListener('change', onSelectChange);
            log('Sistem siap.', 'cyan');
        }
        document.addEventListener('DOMContentLoaded', init);
    </script>

</body>
</html>
