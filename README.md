<!DOCTYPE html>
<html lang="id">

    <head>
        <meta charset="UTF-8">
        <title>Print Vendor & PO</title>

        <style>
            /* ================= SCREEN STYLE ================= */
            body {
                font-family: Arial, sans-serif;
                padding: 20px;
            }

            select,
            button {
                padding: 6px 10px;
                margin-right: 10px;
                margin-bottom: 10px;
            }

            table {
                border-collapse: collapse;
                width: 100%;
                font-size: 12px;
                margin-top: 15px;
            }

            th,
            td {
                border: 1px solid #000;
                padding: 6px;
                vertical-align: top;
            }

            th {
                background: #f2f2f2;
                text-align: center;
            }

            img {
                max-width: 100px;
            }

            /* ================= PRINT STYLE ================= */
            @media print {
                body {
                    padding: 0;
                }

                select,
                button {
                    display: none;
                }

                h3 {
                    display: none;
                    /* sembunyikan judul saat print */
                }

                table {
                    font-size: 11px;
                    page-break-inside: auto;
                }

                tr {
                    page-break-inside: avoid;
                    page-break-after: auto;
                }

                th {
                    background: #ddd !important;
                    -webkit-print-color-adjust: exact;
                    print-color-adjust: exact;
                }
            }

            #poHeader {
                text-align: center;
            }

            table th,
            table td {
                border: 1px solid #000;
                padding: 8px;
                /* padding lebih lega */
                vertical-align: middle;
                /* rata tengah vertikal */
                word-wrap: break-word;
                /* supaya teks panjang tidak merusak layout */
            }

            table th {
                background: #f2f2f2;
                text-align: center;
            }

            table td:nth-child(4),
            table td:nth-child(5) {
                text-align: center;
                vertical-align: middle;
            }

            table td img {
                max-width: 80px;
                /* lebih kecil supaya rapi */
                max-height: 80px;
            }
        </style>
    </head>

    <body>

        <h3>Purchase Order Vendor</h3>

        <select id="vendorSelect">
            <option value="">-- Pilih Vendor --</option>
        </select>

        <select id="poSelect">
            <option value="">-- Pilih PO --</option>
        </select>

        <button onclick="window.print()">Print / Save PDF</button>
        <!-- JUDUL PO -->
        <div id="poHeader" style="margin-top:20px; margin-bottom:10px; display:none;">
            <h2 style="margin:0;">Purchase Order</h2>
            <p style="margin:2px 0;"><strong>Vendor :</strong> <span id="headerVendor"></span></p>
            <p style="margin:2px 0;"><strong>PO :</strong> <span id="headerPO"></span></p>
        </div>

        <!-- Link toko online -->
        <a href="https://boetepaythea-sudo.github.io/Application-New-Product/"
            style="margin-left: 10px; text-decoration: none; color: blue; font-weight: bold;">
            Aplikasi Inspect
        </a>

        <table id="dataTable">
            <thead>
                <tr>
                    <th>Nama Vendor</th>
                    <th>Nama PO</th>
                    <th>Item</th>
                    <th>Qty PO</th>
                    <th>Qty AQL</th>
                    <th>Description</th>
                    <th>Image</th>
                </tr>
            </thead>
            <tbody></tbody>
        </table>

        <script>
            /* ================= DATA ================= */
            const data = {
                "CG2601-02": {
                    Vendor: "V75 Pijar Sukma",
                    items: [
                        {
                            item: "OT-75333-BK",
                            qty: 31,
                            desc: "Sarlet 2 Tone Console Table With Drawer, 23.75 Inch W, Black/Brown, (23.75 Inch W x 10 Inch D x 31.5 Inch H) // Finish Code: B-NAT11/NAT02, Finish Name: Top Natural - Body Black // KD // CBM: 0.06 // Number of Shipping Boxes: 1 // ***DROPSHIP PACKAGING REQUIRED*** // ***ISTA 3A PACKAGING REQUIRED*** // ***ANTI TIP KIT REQUIRED***",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/OT-75333-BK_001.jpg"
                        },
                        {
                            item: "OT-75333-NV",
                            qty: 31,
                            desc: "Sarlat 2 Tone Console Table With Drawer, 23.75 Inch W, Navy/Brown, (23.75 Inch W x 10 Inch D x 31.5 Inch H) // Finish Code: B-BM04/NAT02, Finish Name: Top Natural - Body Navy // KD // CBM: 0.06 // Number of Shipping Boxes: 1 // ***DROPSHIP PACKAGING REQUIRED*** // ***ISTA 3A PACKAGING REQUIRED*** // ***ANTI TIP KIT REQUIRED***",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/OT-75333-NV_001.jpg"
                        },
                        {
                            item: "OT-75333-WH",
                            qty: 21,
                            desc: "Sarlet 2 Tone Console Table With Drawer, 23.75 Inch W, White/Brown, (23.75 Inch W x 10 Inch D x 31.5 Inch H) // Finish Code: B-BM01/NAT02, Finish Name: Top Natural - Body White // KD // CBM: 0.06 // Number of Shipping Boxes: 1 // ***DROPSHIP PACKAGING REQUIRED*** // ***ISTA 3A PACKAGING REQUIRED*** // ***ANTI TIP KIT REQUIRED***",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/OT-75333-WH_001.jpg"
                        },
                        {
                            item: "TT-DU-75008-LB",
                            qty: 29,
                            desc: "Dumaine Bedside Table (15.75x11.81x25.59)   //  Material: Bayur Wood / Top MDF  //  Color: Light Blue (W9.L2+G9)  //  CBM: 0.066  //  Packaging: Carton Box 200 PSI / 5 ply / Plastic wrap around items + Paper oil warp around items+ foam protection + corner plastic protection  //  Master Carton:   //  ***DROPSHIP PACKAGING REQUIRED***",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-DU-75008-LB_001.jpg"
                        },
                        {
                            item: "TT-DU-75008-WH",
                            qty: 21,
                            desc: "Dumaine Bedside Table (15.75x11.81x25.59)   //  Material: Bayur Wood / Top MDF  //  Color: White (BA+WBSemi)  //  CBM: 0.066  //  Packaging: Carton Box 200 PSI / 5 ply / Plastic wrap around items + Foamsheet warp around items + foam protection + corner plastic protection  //  Master Carton:   //  ***DROPSHIP PACKAGING REQUIRED***",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-DU-75008-WH_001.jpg"
                        },
                        {
                            item: "TT-JO-75007-BL",
                            qty: 52,
                            desc: "Josephine Console Table, 24 Inch x10 Inch x31.5 Inch  (23.62x9.84x31.5)   //  Material: Bayur Wood / Top MDF  //  Color: Black (B-W48L2+WBSEMI/PG9)  //  CBM: 0.07  //  Packaging: Carton Box 200 PSI / 5 ply / Plastic wrap around items + Paper oil warp around items+ foam protection + corner plastic protection  //  Master Carton:   //  ***DROPSHIP PACKAGING REQUIRED***",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-JO-75007-BL_001.jpg"
                        },
                        {
                            item: "TT-JO-75007-LB",
                            qty: 26,
                            desc: "Josephine 24 Inch x10 Inch x31.5 Inch  Console Table (23.62x9.84x31.5)   //  Material: Bayur Wood / Top MDF  //  Color: Light Blue (B-W9.L2+G9/PG9)  //  CBM: 0.07  //  Packaging: Carton Box 200 PSI / 5 ply / Plastic wrap around items + Paper oil warp around items+ foam protection + corner plastic protection  //  Master Carton:   //  ***DROPSHIP PACKAGING REQUIRED***",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-JO-75007-LB_001.jpg"
                        },
                        {
                            item: "TT-JO-75007-WH",
                            qty: 32,
                            desc: "Josephine 24 Inch x10 Inch x31.5 Inch  Console Table (23.62x9.84x31.5)   //  Material: Bayur Wood / Top MDF  //  Color: White (B-CA.L3+G9/PO3)  //  CBM: 0.07  //  Packaging: Carton Box 200 PSI / 5 ply / Plastic wrap around items + Foamsheet warp around items + foam protection + corner plastic protection  //  Master Carton:   //  ***DROPSHIP PACKAGING REQUIRED***",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-JO-75007-WH_001.jpg"
                        }
                    ]
                },
                "CG2601-03": {
                    Vendor: "V68 PT. FURNILAC PRIMAGUNA",
                    items: [
                        {
                            item: "ST-68DR16-WN",
                            qty: 25,
                            desc: "16 Inch Cinched Wood Drum Table, Walnut (16x16x23.5) // Material: Wood, MDF // CBM: 0.1725 // Packaging: Inch Drop ship packaging Inch required 5 ply outer craft 200 Styrofoam 3 cm",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/ST-68DR16-WN_001.jpg"
                        },
                        {
                            item: "TT-VC-AD301-BK",
                            qty: 25,
                            desc: "Auburn Traditional One Drawer Wooden Accent Side Table (17.0x14.9x23.4)   //  Material: MDF  //  CBM: 0.1687  //  Packaging: Brown carton 5 ply outer craft 200 Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s Auburn Traditional One Drawer Wooden Accent Side Table-Black (17x15x23) Material/Color:Bayur Wood and Mdf E2/Black..CBM:0.17 Packing:Box K#200+Styrofoam 3cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-AD301-BK_001.jpg"
                        },
                        {
                            item: "TT-VC-AD301-BR",
                            qty: 25,
                            desc: "Auburn Traditional One Drawer Wooden Accent Side Table (17.0x14.9x23.4)   //  Material: MDF, Bayur Wood  //  CBM: 0.1687  //  Packaging: Brown carton  5 ply outer craft 200  Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s Auburn Traditional One Drawer Wooden Accent Side Table-Brown (17x15x23) Material/Color:Bayur Wood and Mdf E2 / Brown CBM:0.17 Packing:Box K#200+Styrofoam 2cm Protection***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-AD301-BR_001.jpg"
                        },
                        {
                            item: "TT-VC-HP325-BK",
                            qty: 60,
                            desc: "Hooper 2 Drawer Wooden Accent Side Table (17.9x14.9x22.0)   //  Material: MDF  //  CBM: 0.173  //  Packaging: Brown carton 5 ply outer craft 200 Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s Hooper 2 Drawer Wooden Accent Side Table-Black..(18x15x22) Material/Color:Bayur Wood and Mdf E2/Black..CBM:0.17 Packing:Box K#200+Styrofoam 3cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-HP325-BK_001.jpg"
                        },
                        {
                            item: "TT-VC-YK339-BR",
                            qty: 60,
                            desc: "York Three Drawer Wooden Accent Side Table (18.5x14.9x22.9)   //  Material: MDF  //  CBM: 0.1787  //  Packaging: Brown carton 5 ply outer craft 200 Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s York 3 Drawer Wooden Accent Side Table-Brown (19x15x23) Material/Color:Bayur Wood and Mdf E2/Brown..CBM:0.18 Packing:Box K#200+Styrofoam 3cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-YK339-BR_001.jpg"
                        },
                        {
                            item: "TT-VC-YK339-WH",
                            qty: 150,
                            desc: "York Three Drawer Wooden Accent Side Table (18.5x14.9x22.9)   //  Material: MDF, Acacia Wood  //  CBM: 0.1787  //  Packaging: Brown carton  5 ply outer craft 200  Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s York 3 Drawer Wooden Accent Side Table-White (19x15x23) Material/Color:Bayur Wood and Mdf E2/White..CBM:0.17 Packing:Box K#200+Styrofoam 2cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-YK339-WH_001.jpg"
                        },
                        {
                            item: "VC-HP325-NV",
                            qty: 35,
                            desc: "Hooper Two Drawer Wooden Accent Side Table, Navy, (18 Inch W x 15 Inch D x 22 Inch H) // CBM: 0.1686 // Packaging: Brown carton, 5 ply outer craft 200, Styrofoam 3 cm (1pc/case) // Materials: Bayur Wood and Mdf E2 // Finish Color: Navy // ***ISTA 3A Dropship Packaging Required***",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/VC-HP325-NV_001.jpg"
                        }
                    ]
                },
                "CG2601-04": {
                    Vendor: "V68 PT. FURNILAC PRIMAGUNA",
                    items: [
                        {
                            item: "ST-68DR16-WN",
                            qty: 25,
                            desc: "16 Inch Cinched Wood Drum Table, Walnut (16x16x23.5) // Material: Wood, MDF // CBM: 0.1725 // Packaging: Inch Drop ship packaging Inch required 5 ply outer craft 200 Styrofoam 3 cm",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/ST-68DR16-WN_001.jpg"
                        },
                        {
                            item: "TT-VC-AD301-BK",
                            qty: 25,
                            desc: "Auburn Traditional One Drawer Wooden Accent Side Table (17.0x14.9x23.4)   //  Material: MDF  //  CBM: 0.1687  //  Packaging: Brown carton 5 ply outer craft 200 Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s Auburn Traditional One Drawer Wooden Accent Side Table-Black (17x15x23) Material/Color:Bayur Wood and Mdf E2/Black..CBM:0.17 Packing:Box K#200+Styrofoam 3cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-AD301-BK_001.jpg"
                        },
                        {
                            item: "TT-VC-AD301-BR",
                            qty: 25,
                            desc: "Auburn Traditional One Drawer Wooden Accent Side Table (17.0x14.9x23.4)   //  Material: MDF, Bayur Wood  //  CBM: 0.1687  //  Packaging: Brown carton  5 ply outer craft 200  Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s Auburn Traditional One Drawer Wooden Accent Side Table-Brown (17x15x23) Material/Color:Bayur Wood and Mdf E2 / Brown CBM:0.17 Packing:Box K#200+Styrofoam 2cm Protection***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-AD301-BR_001.jpg"
                        },
                        {
                            item: "TT-VC-HP325-BK",
                            qty: 60,
                            desc: "Hooper 2 Drawer Wooden Accent Side Table (17.9x14.9x22.0)   //  Material: MDF  //  CBM: 0.173  //  Packaging: Brown carton 5 ply outer craft 200 Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s Hooper 2 Drawer Wooden Accent Side Table-Black..(18x15x22) Material/Color:Bayur Wood and Mdf E2/Black..CBM:0.17 Packing:Box K#200+Styrofoam 3cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-HP325-BK_001.jpg"
                        },
                        {
                            item: "TT-VC-YK339-BR",
                            qty: 60,
                            desc: "York Three Drawer Wooden Accent Side Table (18.5x14.9x22.9)   //  Material: MDF  //  CBM: 0.1787  //  Packaging: Brown carton 5 ply outer craft 200 Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s York 3 Drawer Wooden Accent Side Table-Brown (19x15x23) Material/Color:Bayur Wood and Mdf E2/Brown..CBM:0.18 Packing:Box K#200+Styrofoam 3cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-YK339-BR_001.jpg"
                        },
                        {
                            item: "TT-VC-YK339-WH",
                            qty: 150,
                            desc: "York Three Drawer Wooden Accent Side Table (18.5x14.9x22.9)   //  Material: MDF, Acacia Wood  //  CBM: 0.1787  //  Packaging: Brown carton  5 ply outer craft 200  Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s York 3 Drawer Wooden Accent Side Table-White (19x15x23) Material/Color:Bayur Wood and Mdf E2/White..CBM:0.17 Packing:Box K#200+Styrofoam 2cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-YK339-WH_001.jpg"
                        },
                        {
                            item: "VC-HP325-NV",
                            qty: 35,
                            desc: "Hooper Two Drawer Wooden Accent Side Table, Navy, (18 Inch W x 15 Inch D x 22 Inch H) // CBM: 0.1686 // Packaging: Brown carton, 5 ply outer craft 200, Styrofoam 3 cm (1pc/case) // Materials: Bayur Wood and Mdf E2 // Finish Color: Navy // ***ISTA 3A Dropship Packaging Required***",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/VC-HP325-NV_001.jpg"
                        }
                    ]
                },
                "CG2601-05": {
                    Vendor: "V68 PT. FURNILAC PRIMAGUNA",
                    items: [
                        {
                            item: "OT-68RA52-NT",
                            qty: 25,
                            desc: "Raffia Wrapped K/D Console Table with Shelf, Natural (47.0x15.0x30.0) // Material: Raffia, MDF // CBM: 0.2022 // Packaging: Brown carton 5 ply outer craft 200 Styrofoam 3 cm // ***DROPSHIP PACKAGING REQUIRED*** // KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/OT-68RA52-NT_001.jpg"
                        },
                        {
                            item: "TT-VC-AD301-WH",
                            qty: 25,
                            desc: "Auburn Traditional One Drawer Wooden Accent Side Table (17.0x14.9x23.4)   //  Material: MDF  //  CBM: 0.1687  //  Packaging: Brown carton  5 ply outer craft 200  Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s Auburn Traditional One Drawer Wooden Accent Side Table-White (17x15x23) Material/Color:Bayur Wood and Mdf E2 / White CBM:0.17 Packing:Box K#200+Styrofoam 2cm Protection***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-AD301-WH_001.jpg"
                        },
                        {
                            item: "TT-VC-HP325-BR",
                            qty: 40,
                            desc: "Hooper Two Drawer Wooden Accent Side Table, Brown (17.9x14.9x22.0)   //  Material: Bayur Wood, MDF  //  CBM: 0.173  //  Packaging: Brown carton  5 ply outer craft 200  Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s Hooper 2 Drawer Wooden Accent Side Table-Brown (18x15x22) Material/Color:Bayur Wood and Mdf E2/Brown..CBM:0.17 Packing:Box K#200+Styrofoam 3cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-HP325-BR_001.jpg"
                        },
                        {
                            item: "TT-VC-HP325-WH",
                            qty: 25,
                            desc: "Hooper 2 Drawer Wooden Accent Side Table (17.9x14.9x22.0)   //  Material: MDF, Acacia Wood  //  CBM: 0.173  //  Packaging: Brown carton 5 ply outer craft 200 Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s Hooper 2 Drawer Wooden Accent Side Table-White (18x15x22) Material/Color:Bayur Wood and Mdf E2/White..CBM:0.17 Packing:Box K#200+Styrofoam 3cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-HP325-WH_001.jpg"
                        },
                        {
                            item: "TT-VC-YK339-NV",
                            qty: 115,
                            desc: "York Three Drawer Wooden Accent Side Table (18.5x14.9x22.9)   //  Material: MDF  //  CBM: 0.1787  //  Packaging: Brown carton 5 ply outer craft 200 Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s York 3 Drawer Wooden Accent Side Table-Navy Blue (19x15x23) Material/Color:Bayur Wood and Mdf E2/Navy Blue..CBM:0.18 Packing:Box K#200+Styrofoam 3cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-YK339-NV_001.jpg"
                        },
                        {
                            item: "TT-VC-YK339-OR",
                            qty: 25,
                            desc: "York Three Drawer Wooden Accent Side Table (18.5x14.9x22.9)   //  Material: MDF  //  CBM: 0.1787  //  Packaging: Brown carton 5 ply outer craft 200 Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s York 3 Drawer Wooden Accent Side Table-Orange..(19x15x23) Material/Color : Bayur Wood and Mdf E2 / Orange, CBM: 0.17 Packing : Box K#200 + Protection***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-YK339-OR_001.jpg"
                        },
                        {
                            item: "VC-HP325-GW",
                            qty: 25,
                            desc: "Hooper Two Drawer Wooden Accent Side Table, Gray Wash (17.9x14.9x22.0)   //  Material: Bayur Wood, MDF  //  CBM: 0.1686  //  Packaging: Brown carton   5 ply outer craft 200   Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s Hooper 2 Drawer Wooden Accent Side Table-Wheat..(18x15x22) Material/Color:Bayur Wood and Mdf E2/Wheat..CBM:0.17 Packing:Box K#200+Styrofoam 3cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/VC-HP325-GW_001.jpg"
                        },
                        {
                            item: "VC-YK339-BL",
                            qty: 30,
                            desc: "York Three Drawer Wooden Accent Side Table, 18.5 Inch W, Blue, (18.5 Inch W x 15 Inch D x 23 Inch H) // //Materials: Solid Bayur Wood + Mdf E2 + Solid Meranti (NO VENEER) // Finish Code: BNV/02, Finish Name: Northern Air // Set Up  // CBM: 0.1787 // Number of Shipping Boxes: 1 // ***DROPSHIP PACKAGING REQUIRED*** //  ***ISTA 3A PACKAGING REQUIRED*** //",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/VC-YK339-BL_001.jpg"
                        },
                        {
                            item: "VC-YK339-GW",
                            qty: 25,
                            desc: "York Three Drawer Wooden Accent Side Table (18.5x14.9x22.9)   //  Material: MDF, Acacia Wood  //  CBM: 0.1787  //  Packaging: Brown carton  5 ply outer craft 200  Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s York 3 Drawer Wooden Accent Side Table- Gray Wash  (19x15x23) Material/Color:Bayur Wood and Mdf E2/Wheat..CBM:0.17 Packing:Box K#200+Styrofoam 2cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/VC-YK339-GW_001.jpg"
                        },
                        {
                            item: "VC-YK339-PK",
                            qty: 38,
                            desc: "York Three Drawer Accent Side Table, 18.5 Inch W, Pink, (18.5 Inch W x 15 Inch D x 23 Inch H) //  // Materials: Bayur Wood + MDF // Finish Code: SW 6296, Finish Name: Fading Rose // Set Up  // CBM: 0.1787 // Number of Shipping Boxes: 1 // ***DROPSHIP PACKAGING REQUIRED*** //",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/VC-YK339-PK_001.jpg"
                        }
                    ]
                },
                "CG2601-06": {
                    Vendor: "V68 PT. FURNILAC PRIMAGUNA",
                    items: [
                        {
                            item: "OT-68RA52-NT",
                            qty: 25,
                            desc: "Raffia Wrapped K/D Console Table with Shelf, Natural (47.0x15.0x30.0) // Material: Raffia, MDF // CBM: 0.2022 // Packaging: Brown carton 5 ply outer craft 200 Styrofoam 3 cm // ***DROPSHIP PACKAGING REQUIRED*** // KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/OT-68RA52-NT_001.jpg"
                        },
                        {
                            item: "TT-VC-AD301-WH",
                            qty: 25,
                            desc: "Auburn Traditional One Drawer Wooden Accent Side Table (17.0x14.9x23.4)   //  Material: MDF  //  CBM: 0.1687  //  Packaging: Brown carton  5 ply outer craft 200  Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s Auburn Traditional One Drawer Wooden Accent Side Table-White (17x15x23) Material/Color:Bayur Wood and Mdf E2 / White CBM:0.17 Packing:Box K#200+Styrofoam 2cm Protection***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-AD301-WH_001.jpg"
                        },
                        {
                            item: "TT-VC-HP325-BR",
                            qty: 40,
                            desc: "Hooper Two Drawer Wooden Accent Side Table, Brown (17.9x14.9x22.0)   //  Material: Bayur Wood, MDF  //  CBM: 0.173  //  Packaging: Brown carton  5 ply outer craft 200  Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s Hooper 2 Drawer Wooden Accent Side Table-Brown (18x15x22) Material/Color:Bayur Wood and Mdf E2/Brown..CBM:0.17 Packing:Box K#200+Styrofoam 3cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-HP325-BR_001.jpg"
                        },
                        {
                            item: "TT-VC-HP325-WH",
                            qty: 25,
                            desc: "Hooper 2 Drawer Wooden Accent Side Table (17.9x14.9x22.0)   //  Material: MDF, Acacia Wood  //  CBM: 0.173  //  Packaging: Brown carton 5 ply outer craft 200 Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s Hooper 2 Drawer Wooden Accent Side Table-White (18x15x22) Material/Color:Bayur Wood and Mdf E2/White..CBM:0.17 Packing:Box K#200+Styrofoam 3cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-HP325-WH_001.jpg"
                        },
                        {
                            item: "TT-VC-YK339-NV",
                            qty: 100,
                            desc: "York Three Drawer Wooden Accent Side Table (18.5x14.9x22.9)   //  Material: MDF  //  CBM: 0.1787  //  Packaging: Brown carton 5 ply outer craft 200 Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s York 3 Drawer Wooden Accent Side Table-Navy Blue (19x15x23) Material/Color:Bayur Wood and Mdf E2/Navy Blue..CBM:0.18 Packing:Box K#200+Styrofoam 3cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-YK339-NV_001.jpg"
                        },
                        {
                            item: "TT-VC-YK339-OR",
                            qty: 25,
                            desc: "York Three Drawer Wooden Accent Side Table (18.5x14.9x22.9)   //  Material: MDF  //  CBM: 0.1787  //  Packaging: Brown carton 5 ply outer craft 200 Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s York 3 Drawer Wooden Accent Side Table-Orange..(19x15x23) Material/Color : Bayur Wood and Mdf E2 / Orange, CBM: 0.17 Packing : Box K#200 + Protection***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/TT-VC-YK339-OR_001.jpg"
                        },
                        {
                            item: "VC-HP325-GW",
                            qty: 25,
                            desc: "Hooper Two Drawer Wooden Accent Side Table, Gray Wash (17.9x14.9x22.0)   //  Material: Bayur Wood, MDF  //  CBM: 0.1686  //  Packaging: Brown carton   5 ply outer craft 200   Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s Hooper 2 Drawer Wooden Accent Side Table-Wheat..(18x15x22) Material/Color:Bayur Wood and Mdf E2/Wheat..CBM:0.17 Packing:Box K#200+Styrofoam 3cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/VC-HP325-GW_001.jpg"
                        },
                        {
                            item: "VC-YK339-BL",
                            qty: 30,
                            desc: "York Three Drawer Wooden Accent Side Table, 18.5 Inch W, Blue, (18.5 Inch W x 15 Inch D x 23 Inch H) // //Materials: Solid Bayur Wood + Mdf E2 + Solid Meranti (NO VENEER) // Finish Code: BNV/02, Finish Name: Northern Air // Set Up  // CBM: 0.1787 // Number of Shipping Boxes: 1 // ***DROPSHIP PACKAGING REQUIRED*** //  ***ISTA 3A PACKAGING REQUIRED*** //",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/VC-YK339-BL_001.jpg"
                        },
                        {
                            item: "VC-YK339-GW",
                            qty: 25,
                            desc: "York Three Drawer Wooden Accent Side Table (18.5x14.9x22.9)   //  Material: MDF, Acacia Wood  //  CBM: 0.1787  //  Packaging: Brown carton  5 ply outer craft 200  Styrofoam 3 cm  //  Master Carton:   //  ***Crafted Home Inch s York 3 Drawer Wooden Accent Side Table- Gray Wash  (19x15x23) Material/Color:Bayur Wood and Mdf E2/Wheat..CBM:0.17 Packing:Box K#200+Styrofoam 2cm Protection (1pc/case)***  //    KD",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/VC-YK339-GW_001.jpg"
                        },
                        {
                            item: "VC-YK339-PK",
                            qty: 53,
                            desc: "York Three Drawer Accent Side Table, 18.5 Inch W, Pink, (18.5 Inch W x 15 Inch D x 23 Inch H) //  // Materials: Bayur Wood + MDF // Finish Code: SW 6296, Finish Name: Fading Rose // Set Up  // CBM: 0.1787 // Number of Shipping Boxes: 1 // ***DROPSHIP PACKAGING REQUIRED*** //",
                            image: "https://6694454.app.netsuite.com/c.6694454/item-images/VC-YK339-PK_001.jpg"
                        }
                    ]
                }
            };

            /* ================= ELEMENT ================= */
            const vendorSelect = document.getElementById("vendorSelect");
            const poSelect = document.getElementById("poSelect");
            const tbody = document.querySelector("#dataTable tbody");
            const poHeader = document.getElementById("poHeader");
            const headerVendor = document.getElementById("headerVendor");
            const headerPO = document.getElementById("headerPO");


            /* ================= INIT VENDOR ================= */
            [...new Set(Object.values(data).map(d => d.Vendor))].forEach(v => {
                const opt = document.createElement("option");
                opt.value = v;
                opt.textContent = v;
                vendorSelect.appendChild(opt);
            });

            /* ================= VENDOR CHANGE ================= */
            vendorSelect.addEventListener("change", () => {
                poSelect.innerHTML = '<option value="">-- Pilih PO --</option>';
                tbody.innerHTML = "";

                Object.keys(data).forEach(po => {
                    if (data[po].Vendor === vendorSelect.value) {
                        const opt = document.createElement("option");
                        opt.value = po;
                        opt.textContent = po;
                        poSelect.appendChild(opt);
                    }
                });
            });

            // ===================== AQL & RESULT LOGIC =====================
            function hitungAQL(qty) {
                if (qty >= 2 && qty <= 8) return 2;
                if (qty >= 9 && qty <= 15) return 3;
                if (qty >= 16 && qty <= 25) return 5;
                if (qty >= 26 && qty <= 50) return 8;
                if (qty >= 51 && qty <= 90) return 13;
                if (qty >= 91 && qty <= 150) return 20;
                if (qty >= 151 && qty <= 280) return 32;
                if (qty >= 281 && qty <= 500) return 50;
                return Math.ceil(qty * 0.2);
            }


            /* ================= PO CHANGE ================= */
            poSelect.addEventListener("change", () => {
                tbody.innerHTML = "";
                const po = poSelect.value;
                if (!po) {
                    poHeader.style.display = "none";
                    return;
                }

                // tampilkan header
                poHeader.style.display = "block";
                headerVendor.textContent = data[po].Vendor;
                headerPO.textContent = po;

                data[po].items.forEach(it => {
                    const tr = document.createElement("tr");
                    const qtyAQL = hitungAQL(it.qty);
                    tr.innerHTML = `
            <td>${data[po].Vendor}</td>
            <td>${po}</td>
            <td>${it.item}</td>
            <td>${it.qty}</td>
            <td>${qtyAQL}</td>
            <td>${it.desc}</td>
            <td><img src="${it.image}"></td>
        `;
                    tbody.appendChild(tr);
                });
            });

        </script>

    </body>

</html>
