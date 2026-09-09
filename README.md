[SmartPhone.py](https://github.com/user-attachments/files/31997682/SmartPhone.py)[Address.py](https://github.com/user-attachments/files/31997669/Address.py)[Uploading Address.py
class Addr:
    def __init__(self, name, phone, email, address, group):
        self.name = name         
        self.phone = phone        
        self.email = email       
        self.address = address    
        self.group = group       

    def print_info(self):
        """연락처 정보를 콘솔에 출력"""
        print(f"이름: {self.name}")
        print(f"전화번호: {self.phone}")
        print(f"이메일: {self.email}")
        print(f"주소: {self.address}")
        print(f"그룹(친구/가족): {self.group}")…]()

[Uploading SmartPhone.py…]from Address import Addr

class SmartPhone:
    def __init__(self):
        self.addr_list = []
        self.MAX_SIZE = 10

    def inputAddrData(self):
        if len(self.addr_list) >= self.MAX_SIZE:
            print(">>> 저장 공간이 가득 찼습니다. (최대 10개)")
            return None

        name = input("이름을 입력하세요: ")
        phone = input("전화번호를 입력하세요: ")
        email = input("이메일을 입력하세요: ")
        address = input("주소를 입력하세요: ")
        group = input("그룹(친구/가족)을 입력하세요: ")

        return Addr(name, phone, email, address, group)

    def addAddr(self, addr):
        if addr is None:
            return

        if len(self.addr_list) >= self.MAX_SIZE:
            print(">>> 더 이상 저장할 수 없습니다. (최대 10개)")
            return

        self.addr_list.append(addr)
        print(">>> 데이터가 저장되었습니다.")

    def printAddr(self, addr):
        addr.print_info()

    def printAllAddr(self):
        if not self.addr_list:
            print(">>> 등록된 연락처가 없습니다.")
            return

        for i, addr in enumerate(self.addr_list, start=1):
            print(f"[{i}]")
            self.printAddr(addr)
            print("-" * 25)

    def searchAddr(self):
        if not self.addr_list:
            print(">>> 등록된 연락처가 없습니다.")
            return

        name = input("검색할 이름을 입력하세요: ")
        found = False
        for i, addr in enumerate(self.addr_list, start=1):
            if addr.name == name:
                print(f"[{i}]")
                self.printAddr(addr)
                found = True

        if not found:
            print(f">>> '{name}' 연락처를 찾을 수 없습니다.")

    def deleteAddr(self):
        if not self.addr_list:
            print(">>> 등록된 연락처가 없습니다.")
            return

        name = input("삭제할 이름을 입력하세요: ")
        for i, addr in enumerate(self.addr_list):
            if addr.name == name:
                del self.addr_list[i]
                print(f">>> '{name}' 연락처가 삭제되었습니다.")
                return

        print(f">>> '{name}' 연락처를 찾을 수 없습니다.")

    def editAddr(self):
        if not self.addr_list:
            print(">>> 등록된 연락처가 없습니다.")
            return

        name = input("수정할 연락처의 이름을 입력하세요: ")
        for addr in self.addr_list:
            if addr.name == name:
                print(f">>> '{name}'의 새로운 정보를 입력하세요.")
                addr.phone = input("전화번호를 입력하세요: ")
                addr.email = input("이메일을 입력하세요: ")
                addr.address = input("주소를 입력하세요: ")
                addr.group = input("그룹(친구/가족)을 입력하세요: ")
                print(">>> 연락처가 성공적으로 수정되었습니다.")
                return

        print(f">>> '{name}' 연락처를 찾을 수 없습니다.")()


[SmartPhoneMain.py](https://github.com/user-attachments/files/31997692/SmartPhoneMain.py)
from SmartPhone import SmartPhone

class SmartPhoneMain:
    @staticmethod
    def printMenu():
        print("\n주소관리 메뉴")
        print("1. 연락처 등록")
        print("2. 모든 연락처 출력")
        print("3. 연락처 검색")
        print("4. 연락처 삭제")
        print("5. 연락처 수정")
        print("6. 프로그램 종료")

    @staticmethod
    def start():
        sp = SmartPhone()

        while True:
            SmartPhoneMain.printMenu()
            choice = input("원하는 작업을 선택하세요 (1-6): ").strip()

            if choice == '1':
                new_addr = sp.inputAddrData()
                sp.addAddr(new_addr)

            elif choice == '2':
                sp.printAllAddr()

            elif choice == '3':
                sp.searchAddr()

            elif choice == '4':
                sp.deleteAddr()

            elif choice == '5':
                sp.editAddr()

            elif choice == '6':
                print(">>> 프로그램을 종료합니다.")
                break

            else:
                print(">>> 잘못된 번호입니다. 1부터 6까지의 숫자를 입력하세요.")

if __name__ == "__main__":
    SmartPhoneMain.start()
