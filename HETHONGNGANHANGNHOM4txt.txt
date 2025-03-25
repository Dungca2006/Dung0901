#include<iostream>
#include<fstream>
#include<cctype>
#include<iomanip>
using namespace std;

class taiKhoan {
    int soTaiKhoan;
    char ten[50];
    int soDu;
    char loai;
public:
    void taoTaiKhoan();
    void hienThiTaiKhoan();
    void suaTaiKhoan();
    void napTien(int);
    void rutTien(int);
    void inBaoCao();
    int laySoTaiKhoan();
    int laySoDu();
    char layLoaiTaiKhoan();
};

void taiKhoan::taoTaiKhoan() {
    cout << "\nNhap so tai khoan: ";
    cin >> soTaiKhoan;
    cout << "\nNhap ten chu tai khoan: ";
    cin.ignore();
    cin.getline(ten, 50);
    cout << "\nNhap loai tai khoan (s - tiet kiem, c - thanh toan): ";
    cin >> loai;
    loai = toupper(loai);
    cout << "\nNhap so du khoi tao (500 tro len cho Tai khoan Tiet kiem, 1000 tro len cho Tai khoan Thanh toan): ";
    cin >> soDu;
    cout << "\n\nTao tai khoan thanh cong...";
}

void taiKhoan::hienThiTaiKhoan() {
    cout << "\nSo tai khoan: " << soTaiKhoan;
    cout << "\nTen chu tai khoan: " << ten;
    cout << "\nLoai tai khoan: " << loai;
    cout << "\nSo du tai khoan: " << soDu;
}

void taiKhoan::suaTaiKhoan() {
    cout << "\nSo tai khoan: " << soTaiKhoan;
    cout << "\nSua ten chu tai khoan: ";
    cin.ignore();
    cin.getline(ten, 50);
    cout << "\nSua loai tai khoan: ";
    cin >> loai;
    loai = toupper(loai);
    cout << "\nSua so du tai khoan: ";
    cin >> soDu;
}

void taiKhoan::napTien(int x) {
    soDu += x;
}

void taiKhoan::rutTien(int x) {
    soDu -= x;
}

void taiKhoan::inBaoCao() {
    cout << soTaiKhoan << setw(10) << " " << ten << setw(10) << " " << loai << setw(6) << soDu << endl;
}

int taiKhoan::laySoTaiKhoan() {
    return soTaiKhoan;
}

int taiKhoan::laySoDu() {
    return soDu;
}

char taiKhoan::layLoaiTaiKhoan() {
    return loai;
}

void themTaiKhoan();
void hienThiTaiKhoanTheoSo(int);
void suaTaiKhoanTheoSo(int);
void xoaTaiKhoanTheoSo(int);
void hienThiTatCaTaiKhoan();
void napRutTien(int, int);

int main() {
    char luaChon;
    int soTaiKhoan;
    while (true) {
        system("color 05");
        system("cls");

        cout << "\t\t\t\tHE THONG NGAN HANG\n";
  

        cout << "\t\t@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@\n";
        cout << "\n\t\tChon 1 de tao moi tai khoan";
        cout << "\n\t\tChon 2 de nap tien";
        cout << "\n\t\tChon 3 de rut tien";
        cout << "\n\t\tChon 4 de xem thong tin tai khoan";
        cout << "\n\t\tChon 5 de xem danh sach tai khoan";
        cout << "\n\t\tChon 6 de xoa tai khoan";
        cout << "\n\t\tChon 7 de sua thong tin tai khoan";
        cout << "\n\t\tChon 8 de thoat";
        cout << "\n\t\t@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@@\n";
        cout << "\n\t\tLua chon: ";
        cin >> luaChon;
        system("cls");

        switch (luaChon) {
            case '1':
                system("color 02");
                themTaiKhoan();
                break;
            case '2':
                system("color 03");
                cout << "\n\n\tNhap so tai khoan: ";
                cin >> soTaiKhoan;
                napRutTien(soTaiKhoan, 1);
                break;
            case '3':
                system("color 06");
                cout << "\n\n\tNhap so tai khoan: ";
                cin >> soTaiKhoan;
                napRutTien(soTaiKhoan, 2);
                break;
            case '4':
                system("color 08");
                cout << "\n\n\tNhap so tai khoan: ";
                cin >> soTaiKhoan;
                hienThiTaiKhoanTheoSo(soTaiKhoan);
                break;
            case '5':
                system("color 9");
                hienThiTatCaTaiKhoan();
                break;
            case '6':
                system("color 10");
                cout << "\n\n\tNhap so tai khoan: ";
                cin >> soTaiKhoan;
                xoaTaiKhoanTheoSo(soTaiKhoan);
                break;
            case '7':
                system("color 11");
                cout << "\n\n\tNhap so tai khoan: ";
                cin >> soTaiKhoan;
                suaTaiKhoanTheoSo(soTaiKhoan);
                break;
            case '8':
                system("color 04");
                cout << "\n\n\tCam on ban da su dung he thong ngan hang!";
                break;
            default:
                cout << "Lua chon khong hop le!\n";
        }
        cin.ignore();
        cin.get();
        if (luaChon == '8') break;
    }
    return 0;
}

void themTaiKhoan() {
    taiKhoan tk;
    ofstream outFile;
    outFile.open("taiKhoan.dat", ios::binary | ios::app);
    tk.taoTaiKhoan();
    outFile.write(reinterpret_cast<char*>(&tk), sizeof(taiKhoan));
    outFile.close();
}

void hienThiTaiKhoanTheoSo(int so) {
    taiKhoan tk;
    bool timThay = false;
    ifstream inFile;
    inFile.open("taiKhoan.dat", ios::binary);
    if (!inFile) {
        cout << "Khong the mo file !! Nhap phim bat ky de thoat...";
        return;
    }
    cout << "\nTHONG TIN SO DU TAI KHOAN\n";
    while (inFile.read(reinterpret_cast<char*>(&tk), sizeof(taiKhoan))) {
        if (tk.laySoTaiKhoan() == so) {
            tk.hienThiTaiKhoan();
            timThay = true;
        }
    }
    inFile.close();
    if (!timThay) cout << "\n\nTai khoan khong ton tai!";
}

void suaTaiKhoanTheoSo(int so) {
    taiKhoan tk;
    bool timThay = false;
    fstream file;
    file.open("taiKhoan.dat", ios::binary | ios::in | ios::out);
    if (!file) {
        cout << "Khong the mo file !! Nhap phim bat ky de thoat...";
        return;
    }
    while (!file.eof() && !timThay) {
        file.read(reinterpret_cast<char*>(&tk), sizeof(taiKhoan));
        if (tk.laySoTaiKhoan() == so) {
            tk.hienThiTaiKhoan();
            cout << "\n\nNhap thong tin moi cho tai khoan: ";
            tk.suaTaiKhoan();
            int viTri = (-1) * static_cast<int>(sizeof(taiKhoan));
            file.seekp(viTri, ios::cur);
            file.write(reinterpret_cast<char*>(&tk), sizeof(taiKhoan));
            cout << "\n\nCap nhat thong tin tai khoan thanh cong!";
            timThay = true;
        }
    }
    file.close();
    if (!timThay) cout << "\n\nTai khoan khong ton tai!";
}

void xoaTaiKhoanTheoSo(int so) {
    taiKhoan tk;
    ifstream inFile;
    ofstream outFile;
    inFile.open("taiKhoan.dat", ios::binary);
    if (!inFile) {
        cout << "Khong the mo file !! Nhap phim bat ky de thoat...";
        return;
    }
    outFile.open("Temp.dat", ios::binary);
    inFile.seekg(0, ios::beg);
    while (inFile.read(reinterpret_cast<char*>(&tk), sizeof(taiKhoan))) {
        if (tk.laySoTaiKhoan() != so) {
            outFile.write(reinterpret_cast<char*>(&tk), sizeof(taiKhoan));
        }
    }
    inFile.close();
    outFile.close();
    remove("taiKhoan.dat");
    rename("Temp.dat", "taiKhoan.dat");
    cout << "\n\nXoa tai khoan thanh cong!";
}

void hienThiTatCaTaiKhoan() {
    taiKhoan tk;
    ifstream inFile;
    inFile.open("taiKhoan.dat", ios::binary);
    if (!inFile) {
        cout << "Khong the mo file !! Nhap phim bat ky de thoat...";
        return;
    }

    cout << "\n\nDANH SACH TAI KHOAN\n";
    cout << "====================================================\n";
    cout << "So tai khoan      Ten              Loai    So du\n";
    cout << "====================================================\n";
    while (inFile.read(reinterpret_cast<char*>(&tk), sizeof(taiKhoan))) {
        tk.inBaoCao();
    }
    inFile.close();
}

void napRutTien(int so, int luaChon) {
    int soTien;
    bool timThay = false;
    taiKhoan tk;
    fstream file;
    file.open("taiKhoan.dat", ios::binary | ios::in | ios::out);
    if (!file) {
        cout << "Khong the mo file !! Nhap phim bat ky de thoat...";
        return;
    }
    while (!file.eof() && !timThay) {
        file.read(reinterpret_cast<char*>(&tk), sizeof(taiKhoan));
        if (tk.laySoTaiKhoan() == so) {
            tk.hienThiTaiKhoan();
            if (luaChon == 1) {
                cout << "\n\n\tNhap so tien muon nap: ";
                cin >> soTien;
                tk.napTien(soTien);
            }
            if (luaChon == 2) {
                cout << "\n\n\tNhap so tien muon rut: ";
                cin >> soTien;
                int soDu = tk.laySoDu() - soTien;
             if ((soDu < 500 && tk.layLoaiTaiKhoan() == 'S') || (soDu < 1000 && tk.layLoaiTaiKhoan() == 'C')) {
                    cout << "So du khong du de rut tien!";
                } else {
                    tk.rutTien(soTien);
                }
            }
            int viTri = (-1) * static_cast<int>(sizeof(taiKhoan));
            file.seekp(viTri, ios::cur);
            file.write(reinterpret_cast<char*>(&tk), sizeof(taiKhoan));
            cout << "\n\nCap nhat tai khoan thanh cong!";
            timThay = true;
        }
    }
    file.close();
    if (!timThay) cout << "\n\nTai khoan khong ton tai!";
}
