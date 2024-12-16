#include <iostream>

template <typename T>
class Array {
private:
    T* data;
    int size;
    int capacity;

    void reallocate(int newCapacity) {
        T* newData = new T[newCapacity];
        for (int i = 0; i < size && i < newCapacity; ++i) {
            newData[i] = data[i];
        }
        delete[] data;
        data = newData;
        capacity = newCapacity;
    }

public:
    Array(int initialSize = 0) : size(0), capacity(initialSize) {
        data = new T[capacity];
    }

    ~Array() {
        delete[] data;
    }

    int GetSize() const {
        return size;
    }

    void Add(const T& value) {
        if (size == capacity) {
            reallocate(capacity == 0 ? 1 : capacity * 2);
        }
        data[size++] = value;
    }

    T& GetAt(int index) {
        if (index < 0 || index >= size) {
            throw std::out_of_range("Index out of range");
        }
        return data[index];
    }

    void RemoveAt(int index) {
        if (index < 0 || index >= size) {
            throw std::out_of_range("Index out of range");
        }
        for (int i = index; i < size - 1; ++i) {
            data[i] = data[i + 1];
        }
        --size;
    }

    int GetUpperBound() const {
        return size - 1;
    }

    void Print() const {
        for (int i = 0; i < size; ++i) {
            std::cout << data[i] << " ";
        }
        std::cout << std::endl;
    }
};

int main() {
    Array<int> arr;
    arr.Add(10);
    arr.Add(20);
    arr.Add(30);

    std::cout << "Array contents:" << std::endl;
    arr.Print();

    arr.RemoveAt(1);
    std::cout << "After removal at index 1:" << std::endl;
    arr.Print();

    return 0;
}
