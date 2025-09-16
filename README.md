# program c++
#include <iostream>
#include <vector>
#include <algorithm>
#include <map>
using namespace std;

// Fungsi Mean
double mean(vector<int> data) {
    double sum = 0;
    for (int x : data) sum += x;
    return sum / data.size();
}

// Fungsi Median
double median(vector<int> data) {
    sort(data.begin(), data.end());
    int n = data.size();
    if (n % 2 == 0)
        return (data[n/2 - 1] + data[n/2]) / 2.0;
    else
        return data[n/2];
}

// Fungsi Modus
int modus(vector<int> data) {
    map<int,int> freq;
    for (int x : data) freq[x]++;

    int mode = data[0], maxFreq = 0;
    for (auto &f : freq) {
        if (f.second > maxFreq) {
            maxFreq = f.second;
            mode = f.first;
        }
    }
    return mode;
}

// Fungsi Kuartil
double kuartil(vector<int> data, int k) {
    sort(data.begin(), data.end());
    int n = data.size();
    double pos = (k * (n + 1)) / 4.0; // posisi kuartil
    int idx = (int)pos;

    if (pos == idx) return data[idx - 1];
    else {
        double d = pos - idx;
        return data[idx - 1] + d * (data[idx] - data[idx - 1]);
    }
}

int main() {
    vector<int> data;
    int n, x;

    cout << "Masukkan jumlah data: ";
    cin >> n;
    cout << "Masukkan data: ";
    for (int i = 0; i < n; i++) {
        cin >> x;
        data.push_back(x);
    }

    cout << "\nMean   = " << mean(data);
    cout << "\nMedian = " << median(data);
    cout << "\nModus  = " << modus(data);
    cout << "\nQ1     = " << kuartil(data, 1);
    cout << "\nQ2     = " << kuartil(data, 2); // sama dengan median
    cout << "\nQ3     = " << kuartil(data, 3) << endl;

    return 0;
}
