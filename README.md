[![Build Status](https://travis-ci.org/wifiphisher/wifiphisher.svg?branch=master)](https://travis-ci.org/wifiphisher/wifiphisher)
[![Documentation Status](https://readthedocs.org/projects/wifiphisher/badge/?version=latest)](http://wifiphisher.readthedocs.io/en/latest/?badge=latest)
![Python Version](https://img.shields.io/badge/python-3.7-blue.svg)
![License](https://img.shields.io/badge/license-GPL-blue.svg)

<p align="center"><img src="https://wifiphisher.github.io/wifiphisher/wifiphisher.png" /></p>

## Giới thiệu
<a href="https://wifiphisher.org">Wifiphisher</a> là một framework Access Point giả mạo (rogue) dùng để tiến hành các cuộc diễn tập red team hoặc kiểm thử bảo mật Wi-Fi. Sử dụng Wifiphisher, các pentester có thể dễ dàng đạt được vị trí man-in-the-middle đối với các client không dây bằng cách thực hiện các cuộc tấn công liên kết Wi-Fi có chủ đích. Wifiphisher còn có thể được dùng để dàn dựng các cuộc tấn công phishing web tùy chỉnh theo nạn nhân nhắm vào các client đã kết nối, nhằm đánh cắp thông tin đăng nhập (ví dụ từ các trang đăng nhập của bên thứ ba hoặc khóa chia sẻ trước WPA/WPA2) hoặc lây nhiễm malware vào các máy trạm nạn nhân.

Wifiphisher là...

* ...mạnh mẽ. Wifiphisher có thể chạy hàng giờ liền bên trong một thiết bị Raspberry Pi
thực thi tất cả các kỹ thuật liên kết Wi-Fi hiện đại (bao gồm "Evil Twin", "KARMA" và "Known Beacons").

* ...linh hoạt. Hỗ trợ hàng chục tham số và đi kèm với một bộ
template phishing do cộng đồng đóng góp cho các kịch bản triển khai khác nhau.

* ...theo module. Người dùng có thể <a href="http://wifiphisher.readthedocs.io/en/latest/extensions.html">viết các module đơn giản hoặc phức tạp</a> bằng Python để mở rộng chức năng của công cụ hoặc <a href="http://wifiphisher.readthedocs.io/en/latest/custom_phishing_scenario.html">tạo các kịch bản phishing tùy chỉnh</a> nhằm tiến hành các cuộc tấn công nhắm mục tiêu cụ thể.

* ...dễ sử dụng. Người dùng nâng cao có thể tận dụng bộ tính năng phong phú mà Wifiphisher cung cấp, nhưng người mới bắt đầu có thể chỉ cần chạy đơn giản "./bin/wifiphisher". Giao diện người dùng dạng văn bản tương tác sẽ hướng dẫn người kiểm thử qua quy trình xây dựng cuộc tấn công.

* ...là kết quả của một nghiên cứu chuyên sâu. Các cuộc tấn công như "Known Beacons" và "Lure10" cũng như các kỹ thuật phishing tân tiến nhất, đã được các nhà phát triển của chúng tôi công bố, và Wifiphisher là công cụ đầu tiên tích hợp chúng.

* ...được hỗ trợ bởi một cộng đồng tuyệt vời gồm các nhà phát triển và người dùng.

* ...miễn phí. Wifiphisher có thể tải xuống miễn phí, và cũng đi kèm với đầy đủ
mã nguồn mà bạn có thể nghiên cứu, thay đổi, hoặc phân phối theo các điều khoản của
giấy phép GPLv3.

## Cách hoạt động

Wi-Fi phishing bao gồm hai bước:

1. Bước đầu tiên liên quan đến quá trình liên kết với các client Wi-Fi
mà họ không hề hay biết, hay nói cách khác, đạt được vị trí man-in-the-middle (MITM). Wifiphisher sử dụng một số kỹ thuật khác nhau để đạt được điều này, bao gồm:
    * Evil Twin, trong đó Wifiphisher tạo ra một mạng không dây giả trông giống với một mạng hợp pháp.
    * KARMA, trong đó Wifiphisher giả dạng thành một mạng công cộng mà các client Wi-Fi lân cận đang tìm kiếm.
    * Known Beacons, trong đó Wifiphisher phát sóng một từ điển các ESSID phổ biến, mà các máy trạm không dây xung quanh có khả năng đã từng kết nối trước đây.

    Đồng thời, Wifiphisher liên tục giả mạo các gói tin "Deauthenticate" hoặc "Disassociate" để phá vỡ các liên kết hiện có và cuối cùng dụ dỗ nạn nhân bằng các kỹ thuật nêu trên.

<p align="center"><img width="70%" src="https://wifiphisher.github.io/wifiphisher/diagram.jpg" /><br /><i>Thực hiện cuộc tấn công MiTM</i></p>

2. (Tùy chọn) Có một số cuộc tấn công khác nhau có thể được thực hiện
một khi Wifiphisher mang lại cho pentester vị trí man-in-the-middle. Ví dụ, người kiểm thử có thể thực hiện dò tìm dữ liệu (sniffing) hoặc quét các máy trạm nạn nhân để tìm lỗ hổng.

    Sử dụng Wifiphisher, các kỹ thuật phishing web nâng cao trở nên khả thi bằng cách thu thập
thông tin từ môi trường mục tiêu và người dùng nạn nhân. Ví dụ, trong một trong
các kịch bản của chúng tôi, Wifiphisher sẽ trích xuất thông tin từ các khung beacon
được phát sóng và header User-Agent của HTTP để hiển thị một bản mô phỏng dựa trên web
của trình quản lý mạng Windows nhằm đánh cắp Khóa chia sẻ trước (PSK).

<p align="center"><img src="https://wifiphisher.github.io/wifiphisher/ss-webphishing.png" /><br /><i>Giả mạo <a href="https://wifiphisher.org/ps/wifi_connect/">trình quản lý mạng dựa trên web</a></i></p>

## Yêu cầu
Sau đây là các yêu cầu để tận dụng tối đa Wifiphisher:

  - Một hệ thống Linux hoạt động tốt. Nhiều người đã làm cho Wifiphisher hoạt động trên nhiều bản phân phối, nhưng Kali Linux là bản phân phối được hỗ trợ chính thức, do đó tất cả các tính năng mới đều được kiểm thử chủ yếu trên nền tảng này.
  - Một adapter mạng không dây hỗ trợ chế độ AP & Monitor và có khả năng injection. Driver phải hỗ trợ netlink.

## Cài đặt

Để cài đặt phiên bản phát triển mới nhất, hãy nhập các lệnh sau:

```bash
git clone https://github.com/wifiphisher/wifiphisher.git # Tải xuống bản sửa đổi mới nhất
cd wifiphisher # Chuyển sang thư mục của công cụ
sudo python setup.py install # Cài đặt các dependency cần thiết
```

Ngoài ra, bạn có thể tải xuống phiên bản ổn định mới nhất từ <a href="https://github.com/wifiphisher/wifiphisher/releases">trang Releases</a>.

## Cách sử dụng

Chạy công cụ bằng cách gõ `wifiphisher` hoặc `python bin/wifiphisher` (từ bên trong thư mục của công cụ).

Khi chạy công cụ mà không có bất kỳ tùy chọn nào, nó sẽ tìm ra các interface phù hợp và hỏi người dùng một cách tương tác để chọn ESSID của mạng mục tiêu (từ một danh sách gồm tất cả các ESSID trong khu vực xung quanh) cũng như một kịch bản phishing để thực hiện. Theo mặc định, công cụ sẽ thực hiện cả tấn công Evil Twin và KARMA.

***

```shell
wifiphisher -aI wlan0 -jI wlan4 -p firmware-upgrade --handshake-capture handshake.pcap
```

Sử dụng wlan0 để tạo Access Point giả mạo và wlan4 cho các cuộc tấn công DoS. Chọn mạng mục tiêu thủ công từ danh sách và thực hiện kịch bản "Firmware Upgrade". Xác minh rằng Khóa chia sẻ trước đã bắt được là chính xác bằng cách đối chiếu với handshake trong file handshake.pcap.

Hữu ích để chọn thủ công các adapter không dây. Kịch bản <a href="https://wifiphisher.org/ps/firmware-upgrade/">"Firmware Upgrade"</a> là một cách dễ dàng để lấy được PSK từ một mạng được bảo vệ bằng mật khẩu.

***

```shell
wifiphisher --essid CONFERENCE_WIFI -p plugin_update -pK s3cr3tp4ssw0rd
```

Tự động chọn các interface phù hợp. Nhắm mục tiêu vào Wi-Fi có ESSID "CONFERENCE_WIFI" và thực hiện kịch bản "Plugin Update". Evil Twin sẽ được bảo vệ bằng mật khẩu với PSK "s3cr3tp4ssw0rd".

Hữu ích đối với các mạng có PSK đã bị lộ (ví dụ tại các hội nghị). Kịch bản <a href="https://wifiphisher.org/ps/plugin_update/">"Plugin Update"</a> cung cấp một cách dễ dàng để khiến nạn nhân tải xuống các file thực thi độc hại (ví dụ malware chứa payload reverse shell).

***

```shell
wifiphisher --essid "FREE WI-FI" -p oauth-login -kB
```

Chỉ cần tạo ra một mạng Wi-Fi mở với ESSID "FREE WI-FI" và thực hiện kịch bản "OAuth Login". Hơn nữa, triển khai kỹ thuật liên kết tự động Wi-Fi "Known Beacons".

Hữu ích đối với nạn nhân tại các khu vực công cộng. Kịch bản <a href="https://wifiphisher.org/ps/oauth-login/">"OAuth Login"</a> cung cấp một cách đơn giản để đánh cắp thông tin đăng nhập từ các mạng xã hội, như Facebook.

Sau đây là tất cả các tùy chọn cùng với mô tả của chúng (cũng có sẵn với `wifiphisher -h`):

| Dạng ngắn | Dạng đầy đủ | Giải thích |
| :----------: | :---------: | :-----------: |
|-h | --help| hiển thị thông báo trợ giúp này và thoát |
|-i INTERFACE| --interface INTERFACE| Chọn thủ công một interface hỗ trợ cả chế độ AP và monitor để tạo AP giả mạo cũng như triển khai các cuộc tấn công Wi-Fi bổ sung từ Extensions (ví dụ: deauth). Ví dụ: -i wlan1 |
|-eI EXTENSIONSINTERFACE| --extensionsinterface EXTENSIONSINTERFACE| Chọn thủ công một interface hỗ trợ chế độ monitor để chạy các extension. Ví dụ: -eI wlan1|
|-aI APINTERFACE| --apinterface APINTERFACE| Chọn thủ công một interface hỗ trợ chế độ AP để tạo một AP. Ví dụ: -aI wlan0|
|-pI INTERFACE| --protectinterface INTERFACE| Chỉ định một hoặc nhiều interface sẽ được bảo vệ kết nối khỏi bị NetworkManager quản lý.|
|-kN| --keepnetworkmanager| Không tắt NetworkManager.|
|-nE| --noextensions| Không tải bất kỳ extension nào.|
|-e ESSID| --essid ESSID| Nhập ESSID của Access Point giả mạo. Tùy chọn này sẽ bỏ qua giai đoạn chọn Access Point. Ví dụ: --essid 'Free WiFi'|
|-pPD PHISHING_PAGES_DIRECTORY|--phishing-pages-directory PHISHING_PAGES_DIRECTORY| Tìm kiếm các trang phishing tại vị trí này|
|-p PHISHINGSCENARIO| --phishingscenario PHISHINGSCENARIO |Chọn kịch bản phishing để chạy. Tùy chọn này sẽ bỏ qua giai đoạn chọn kịch bản. Ví dụ: -p firmware_upgrade|
|-pK PRESHAREDKEY| --presharedkey PRESHAREDKEY| Thêm bảo vệ WPA/WPA2 cho Access Point giả mạo. Ví dụ: -pK s3cr3tp4ssw0rd|
|-qS| --quitonsuccess| Dừng script sau khi lấy được thành công một cặp thông tin đăng nhập.|
|-lC| --lure10-capture| Bắt các BSSID của các AP được phát hiện trong giai đoạn chọn AP. Tùy chọn này là một phần của cuộc tấn công Lure10.
|-lE LURE10_EXPLOIT |--lure10-exploit LURE10_EXPLOIT| Đánh lừa Windows Location Service của người dùng Windows lân cận để tin rằng nó đang ở trong một khu vực đã được bắt trước đó bằng --lure10-capture. Là một phần của cuộc tấn công Lure10.|
|-iAM| --mac-ap-interface| Chỉ định địa chỉ MAC của interface AP. Ví dụ: -iAM 38:EC:11:00:00:00|
|-iEM| --mac-extensions-interface| Chỉ định địa chỉ MAC của interface extensions. Ví dụ: -iEM E8:2A:EA:00:00:00|
|-iNM| --no-mac-randomization| Không thay đổi bất kỳ địa chỉ MAC nào.|
|-hC|--handshake-capture|Bắt các handshake WPA/WPA2 để xác minh mật khẩu. Yêu cầu cowpatty. Ví dụ: -hC capture.pcap|
|-dE ESSID|--deauth-essid ESSID|Deauth tất cả các BSSID trong WLAN có ESSID đó.|
|-dC CHANNELS| --deauth-channels CHANNELS|Các kênh để deauth. Ví dụ: --deauth-channels 1,3,7|
||--logging| Bật ghi log. Đầu ra sẽ được lưu vào file wifiphisher.log.|
|-lP LOGPATH| --logpath LOGPATH| Xác định đường dẫn đầy đủ của file log.|
|-cP CREDENTIAL_LOG_PATH|--credential-log-path CREDENTIAL_LOG_PATH|Xác định đường dẫn đầy đủ của file sẽ lưu trữ bất kỳ thông tin đăng nhập nào bắt được|
|-cM|--channel-monitor|Giám sát xem access point mục tiêu có thay đổi kênh hay không.|
||--payload-path| Bật đường dẫn payload. Dùng cho các kịch bản phục vụ payload.|
|-wP|--wps-pbc|Giám sát xem nút trên phía WPS-PBC Registrar có được nhấn hay không.|
|-wAI|--wpspbc-assoc-interface|Interface WLAN được dùng để liên kết với Access Point WPS.|
|-kB|--known-beacons|Thực hiện kỹ thuật liên kết tự động Wi-Fi known beacons.|
|-fH|--force-hostapd|Buộc sử dụng hostapd đã được cài đặt trên hệ thống.|
||--dnsmasq-conf DNSMASQ_CONF|Xác định đường dẫn đầy đủ của file dnmasq.conf.|
|-dK|--disable-karma|Vô hiệu hóa tấn công KARMA.|
|-pE|--phishing-essid|Xác định ESSID bạn muốn sử dụng cho trang phishing.|


## Ảnh chụp màn hình

<p align="center"><img src="https://wifiphisher.github.io/wifiphisher/ss5.png" /><br /><i>Nhắm mục tiêu vào một access point</i></p>
<p align="center"><img src="https://wifiphisher.github.io/wifiphisher/ss2.png" /><br /><i>Một cuộc tấn công thành công</i></p>
<p align="center"><img src="https://wifiphisher.github.io/wifiphisher/ss7.png" /><br /><i>Giả mạo <a href="https://wifiphisher.org/ps/firmware-upgrade/">trang cấu hình router</a></i></p>
<p align="center"><img src="https://wifiphisher.github.io/wifiphisher/ss6.png" /><br /><i>Giả mạo <a href="https://wifiphisher.org/ps/oauth-login/">trang OAuth Login</a></i></p>
<p align="center"><img src="https://wifiphisher.github.io/wifiphisher/ss4.png" /><br /><i>Giả mạo <a href="https://wifiphisher.org/ps/wifi_connect/">trình quản lý mạng dựa trên web</a></i></p>


## Cần hỗ trợ
Nếu bạn là một nhà phát triển Python hoặc một nhà thiết kế web, bạn có thể giúp chúng tôi cải thiện Wifiphisher. Hãy thoải mái ghé qua <a href="https://github.com/wifiphisher/wifiphisher/issues">bug tracker</a> để xem một số công việc cần làm.

Nếu bạn không biết cách viết code, bạn có thể giúp chúng tôi bằng cách <a href="https://github.com/wifiphisher/wifiphisher/issues">đề xuất cải tiến hoặc báo cáo lỗi</a>. Vui lòng xem qua Hướng dẫn Báo cáo Lỗi và <a href="https://wifiphisher.readthedocs.io/en/latest/faq.html">tài liệu FAQ</a> trước đó. Lưu ý rằng công cụ này không nhằm mục đích thân thiện với script-kiddie. Hãy chắc chắn rằng bạn hiểu cách công cụ hoạt động trước khi mở một issue.

## Ghi công
Script này dựa trên một ý tưởng từ 
href="https://github.com/DanMcInerney">Dan McInerney</a> vào năm 2015.

Danh sách đầy đủ những người đóng góp nằm <a href="https://github.com/wifiphisher/wifiphisher/graphs/contributors">tại đây</a>.

## Giấy phép
Wifiphisher được cấp phép theo giấy phép GPLv3. Xem [LICENSE](LICENSE) để biết thêm thông tin.

## Trạng thái dự án
Phiên bản hiện tại của Wifiphisher là **1.4**. Bạn có thể tải xuống bản phát hành mới nhất từ <a href="https://github.com/wifiphisher/wifiphisher/releases/tag/v1.4">đây</a>. Ngoài ra, bạn có thể lấy phiên bản phát triển mới nhất bằng cách clone repository này.

## Tuyên bố miễn trừ trách nhiệm
* Việc sử dụng Wifiphisher để tấn công các hạ tầng mà không có sự đồng thuận trước có thể được coi là một hành vi bất hợp pháp. Người dùng cuối phải chịu trách nhiệm tuân thủ tất cả các luật địa phương, tiểu bang và liên bang hiện hành. Các tác giả không chịu bất kỳ trách nhiệm pháp lý nào và không chịu trách nhiệm về bất kỳ hành vi lạm dụng hoặc thiệt hại nào gây ra bởi chương trình này.

<b>Lưu ý</b>: Hãy cẩn thận với các trang web giả mạo có liên quan đến Dự án Wifiphisher. Chúng có thể đang phát tán malware.

Để cập nhật tin tức về Wifiphisher, hãy theo dõi chúng tôi trên <a href="https://www.twitter.com/wifiphisher">Twitter</a> hoặc thích trang của chúng tôi trên <a href="https://www.facebook.com/Wifiphisher-129914317622032/">Facebook</a>.
