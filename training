import requests
import re

# Link API cơ bản (không bao gồm giá trị page)
base_api_url = "https://smcc.unestgroup.com/api/content?page={}&pageSize=1000&sortBy=postedAt&desc=true"

# Hàm để lấy dữ liệu từ API cho một trang cụ thể
def get_text_for_page(page):
    api_url = base_api_url.format(page)
    response = requests.get(api_url)

    # Kiểm tra xem yêu cầu có thành công không (status code 200 là thành công)
    if response.status_code == 200:
        # Nội dung của API
        api_content = response.text

        # Regular expression để trích xuất thông tin từ thẻ "link" và "textContent"
        pattern = re.compile(r'"textContent":"([^"]*)"')

        # Tìm kiếm và trích xuất thông tin
        matches = pattern.findall(api_content)

        # Kiểm tra xem có thông tin được tìm thấy không
        if matches:
            # Mở file text.txt với chế độ "w" để ghi mới (xóa nội dung cũ)
            with open("text.txt", "w", encoding="utf-8") as file:
                for i, ( text_content) in enumerate(matches, start=1):
                    # Xuất nội dung thẻ "textContent"
                    file.write(f"\n\nText Content {i}:\n")
                    
                    # Tách dữ liệu ra tối đa 100 ký tự trên mỗi dòng
                    cleaned_content = re.sub(r'[^\w\s]', '', text_content)
                    lines = [cleaned_content[i:i + 100] for i in range(0, len(cleaned_content), 100)]
                    file.write('\n'.join(lines) + '\n')


            print(f"Page {page}: Dữ liệu từ API đã được ghi vào file text.txt.")
        else:
            print(f"Page {page}: Không tìm thấy thông tin trong API.")
    else:
        print(f"Page {page}: Yêu cầu không thành công. Mã trạng thái:", response.status_code)

def get_link_for_page(page):
    api_url = base_api_url.format(page)
    response = requests.get(api_url)

    # Kiểm tra xem yêu cầu có thành công không (status code 200 là thành công)
    if response.status_code == 200:
        # Nội dung của API
        api_content = response.text

        # Regular expression để trích xuất thông tin từ thẻ "link" và "textContent"
        pattern = re.compile(r'],"link":"([^"]*)"')

        # Tìm kiếm và trích xuất thông tin
        matches = pattern.findall(api_content)

        # Kiểm tra xem có thông tin được tìm thấy không
        if matches:
            # Mở file text.txt với chế độ "w" để ghi mới (xóa nội dung cũ)
            with open("link.txt", "w", encoding="utf-8") as file:
                for i, (link) in enumerate(matches, start=1):
                    # Xuất nội dung thẻ "link"
                    file.write(f"\nLink {i}: {link}\n")


            print(f"Page {page}: Dữ liệu từ API đã được ghi vào file text.txt.")
        else:
            print(f"Page {page}: Không tìm thấy thông tin trong API.")
    else:   
        print(f"Page {page}: Yêu cầu không thành công. Mã trạng thái:", response.status_code)

# Lặp qua các trang từ 1 đến 100
for page_number in range(1, 3):
    get_link_for_page(page_number)
    get_text_for_page(page_number)
