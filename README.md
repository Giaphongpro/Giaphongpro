#include <iostream>
#include <conio.h> // Để sử dụng _getch()
#include <cstdlib>
#include <ctime>
#include <thread>
#include <chrono>

using namespace std;

bool gameRunning = true;

void display() {
    cout << "Chạy! Tránh chướng ngại vật!" << endl;
    cout << "Sử dụng phím A (trái) và D (phải) để di chuyển." << endl;
    cout << "Nhấn Q để thoát." << endl;
}

void gameLoop() {
    char playerPos = ' ';
    int score = 0;

    while (gameRunning) {
        // Hiển thị vị trí người chơi
        system("cls"); // Xóa màn hình
        display();
        cout << "Điểm: " << score << endl;
        cout << "Vị trí của bạn: " << playerPos << endl;

        // Chọn ngẫu nhiên vị trí chướng ngại vật
        char obstacle = (rand() % 2 == 0) ? 'X' : ' ';

        cout << "Chướng ngại vật: " << obstacle << endl;

        // Nhập phím
        if (_kbhit()) {
            char ch = _getch();
            if (ch == 'a') {
                playerPos = '<';
            } else if (ch == 'd') {
                playerPos = '>';
            } else if (ch == 'q') {
                gameRunning = false;
            }
        }

        // Kiểm tra va chạm
        if (playerPos == '>' && obstacle == 'X') {
            cout << "Bạn đã va chạm! Game over!" << endl;
            gameRunning = false;
        }

        score++;
        this_thread::sleep_for(chrono::milliseconds(200)); // Tạm dừng một chút
    }
}

int main() {
    srand(static_cast<unsigned int>(time(0))); // Khởi tạo seed cho random
    gameLoop();
    cout << "Điểm cuối: " << score << endl;
    return 0;
}
