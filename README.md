# Datepicker-js-Thai-year
Date Picker เปลี่ยนจากปี ค.ศ เป็น พ.ศ.

## วัตถุประสงค์
เนื่องจากโปรเจ็คที่ทำผู้ใช้งานต้องการใช้ภาษาไทยทั้งหมด รวมทั้งหน่วยและวันเดือนปีต่างๆ ด้วย ในส่วนของ วันเดือนปี ผมได้เลือกให้ JQuery library date picker ตัวนี้ [pickadate.js](https://amsul.ca/pickadate.js/). เพราะดีไซล์ทันสมัย, responsive, ขนาดเล็กเบา. 

## Dependencies
- [JQuery](https://jquery.com/)
- [pickadate.js](https://amsul.ca/pickadate.js/)


## การติดตั้ง
```html
<!-- JQuery -->
<script src="Your_Path_To/jquery-3.7.0.min.js"></script>

<!-- Pickadate -->
<!-- CSS -->
    <link rel="stylesheet" href="Your_Path_To/pickadate/lib/themes/default.css">
    <link rel="stylesheet" href="Your_Path_To/pickadate/lib/themes/default.date.css">

<!-- JavaScript -->
    <script src="Your_Path_To/pickadate/lib/picker.js"></script>
    <script src="Your_Path_To/pickadate/lib/picker.date.js"></script>
```

## การเรียกใช้
```html
<script>
    $('.datepicker').pickadate({
        max: true, //ไม่สามารถเลือกวันเดือนปี เกินวันที่ปัจจุบันได้
        monthsFull: ['มกราคม', 'กุมภาพันธ์', 'มีนาคม', 'เมษายน', 'พฤษภาคม', 'มิถุนายน', 'กรกฎาคม', 'สิงหาคม', 'กันยายน', 'ตุลาคม', 'พฤศจิกายน', 'ธันวาคม'],
        monthsShort: ['ม.ค.', 'ก.พ.', 'มี.ค.', 'เม.ย.', 'พ.ค.', 'มิ.ย.', 'ก.ค.', 'ส.ค.', 'ก.ย.', 'ต.ค.', 'พ.ย.', 'ธ.ค.'],
        weekdaysFull: ['อาทิตย์', 'จันทร์', 'อังคาร', 'พุธ', 'พฤหัสบดี', 'ศุกร์', 'เสาร์'],
        weekdaysShort: ['อา.', 'จ.', 'อ.', 'พ.', 'พฤ.', 'ศ.', 'ส.'],
        today: 'วันนี้',
        clear: 'ลบ',
        format: 'dd-mm-yyyy',
        formatSubmit: 'dd-mm-yyyy',
        selectMonths: true, //เลือกเดือนได้
        selectYears: 5, //เลือกปีได้ 5ปี (true, ค่าเริ่มต้น 10ปี )
        onRender: function () {
            var yearDropdown = this.$root.find('.picker__select--year');
            if (yearDropdown.length > 0) {
                yearDropdown.find('option').each(function () {
                    var westernYear = parseInt($(this).text());
                    var buddhistYear = westernYear + 543; // แปลงเป็น พ.ศ.
                    $(this).text(buddhistYear);
                });
            }
        },
        onClose: function () {
            // จัดรูปแบบค่าฟิลด์อินพุตหลังจากที่ตัวเลือกปิด
            var selectedDate = this.get('select', 'dd-mm-yyyy'); // รับวันที่เลือก
            var parts = selectedDate.split('-'); // แยกส่วนวันที่
            var buddhistYear = parseInt(parts[2]) + 543; // แปลงเป็น พ.ศ. (เนื่องจากค่าใน input จะยังเป็น ค.ศ. จึงต้องแปลงอีกรอบ)
            var formattedDate = buddhistYear + '-' + parts[1] + '-' + parts[0]; // จัดวันที่ใหม่ในรูปแบบที่ MySQL รองรับ
            this.$node.val(formattedDate); // อัปเดตค่าอินพุต
        }
    });
    
</script>

## ของใหม่ หรือปรับแก้

<script>
$('.datepicker').pickadate({
    max: true, //ไม่สามารถเลือกวันเดือนปี เกินวันที่ปัจจุบันได้
    monthsFull: ['มกราคม', 'กุมภาพันธ์', 'มีนาคม', 'เมษายน', 'พฤษภาคม', 'มิถุนายน', 'กรกฎาคม', 'สิงหาคม', 'กันยายน', 'ตุลาคม', 'พฤศจิกายน', 'ธันวาคม'],
    monthsShort: ['ม.ค.', 'ก.พ.', 'มี.ค.', 'เม.ย.', 'พ.ค.', 'มิ.ย.', 'ก.ค.', 'ส.ค.', 'ก.ย.', 'ต.ค.', 'พ.ย.', 'ธ.ค.'],
    weekdaysFull: ['อาทิตย์', 'จันทร์', 'อังคาร', 'พุธ', 'พฤหัสบดี', 'ศุกร์', 'เสาร์'],
    weekdaysShort: ['อา.', 'จ.', 'อ.', 'พ.', 'พฤ.', 'ศ.', 'ส.'],
    today: 'วันนี้',
    clear: 'ลบ',
    format: 'dd-mm-yyyy',
    formatSubmit: 'dd-mm-yyyy',
    selectMonths: true, //เลือกเดือนได้
    selectYears: 5, //เลือกปีได้ 5ปี (true, ค่าเริ่มต้น 10ปี )
    onRender: function () {
        var yearDropdown = this.$root.find('.picker__select--year');
        if (yearDropdown.length > 0) {
            yearDropdown.find('option').each(function () {
                var westernYear = parseInt($(this).text());
                var buddhistYear = westernYear + 543; // แปลงเป็น พ.ศ.
                $(this).text(buddhistYear);
            });
        }
    },
    onClose: function () {
        // จัดรูปแบบค่าฟิลด์อินพุตหลังจากที่ตัวเลือกปิด
        var selectedDate = this.get('select', 'dd-mm-yyyy'); // รับวันที่เลือก
        var parts = selectedDate.split('-'); // แยกส่วนวันที่
        var buddhistYear = parseInt(parts[2]) + 543; // แปลงเป็น พ.ศ.
        var formattedDate = parts[0] + '-' + parts[1] + '-' + buddhistYear; // จัดวันที่ใหม่

        // ส่งค่าวันที่ใหม่ไปยังฟอร์มหรือที่ต้องการในที่นี้
        // $("#your_date_input").val(formattedDate);
        this.$node.val(formattedDate);
    }
});
</script>

```
php
if (!function_exists('formatDateToThai')) {
    function formatDateToThai($gregorianDate) {
        // แปลงวันที่เข้ารูปแบบ DateTime
        $date = new DateTime($gregorianDate);

        // หาปีเท่ากับ 543 ปีมาเพิ่มให้กับปีของวันที่เริ่มต้น
        $buddhistYear = $date->format('Y') + 543;

        // ดึงชื่อเดือนเป็นภาษาไทย
        $monthNamesThai = [
            1 => 'มกราคม', 2 => 'กุมภาพันธ์', 3 => 'มีนาคม', 4 => 'เมษายน',
            5 => 'พฤษภาคม', 6 => 'มิถุนายน', 7 => 'กรกฎาคม', 8 => 'สิงหาคม',
            9 => 'กันยายน', 10 => 'ตุลาคม', 11 => 'พฤศจิกายน', 12 => 'ธันวาคม'
        ];

        $month = $monthNamesThai[(int)$date->format('m')];

        // สร้างรูปแบบ "วันที่ ... เดือน ... พ.ศ. ..."
        $formattedDate = "วันที่ " . $date->format('d') . " เดือน " . $month . " พ.ศ. " . $buddhistYear;

        return $formattedDate;

        // ตัวอย่างการใช้งาน
        // $gregorianDate = "2023-10-31"; // วันที่เริ่มต้นในรูปแบบ "yyyy-MM-dd"
        // $thaiDate = formatDateToThai($gregorianDate);
        // echo $thaiDate; // พิมพ์ "วันที่ 31 เดือน ตุลาคม พ.ศ. 2566"
    }
}
php
