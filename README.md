# MenuDrivenArray
In this program, the operations on array are shown like sum of array, union of two arrays and so on.


//*******************************************************************************


//Menu Driver program using Array

#include <iostream>

using namespace std;

class Array{
    //Required data members
private:    
    int *A;
    int size;
    int length;
    void swap(int *x, int *y);
public:
//Comstructors
    Array(){
        size=10;
        length=0;
        A=new int[size];
    }
    Array(int sz){
        size=sz;
        A=new int[size];
        length=0;
    }
    
//Destructor    
    ~Array(){
        delete []A;
    }
//Operations    
    void Display();
    void Append(int x);
    void Insert(int index, int x);
    int Delete(int index);
    int LinearSearch(int key);
    int BinarySearch(int key);
    int Get(int index);
    void set(int index, int x);
    int Max();
    int Min();
    int sum();
    float Avg();
    void Reverse();
    void Reverse2();
    void InsertSort(int x);
    int isSorted();
    void Rearrange();
    Array * Merge(Array arr2);
    Array *Union(Array arr2);
    Array *Intersection(Array arr2);
    Array *Difference(Array arr2);
};

//Function for displaying elements of an array
void Array::Display(){
    cout<<"Elements are "<<endl;
    for(int i=0; i<length; i++){
        cout<<A[i]<<" ";
    }
}

//Function for appending a element in the end of the array
void Array::Append(int x){
    if(length<size){
        A[length++]=x;
    }
}
//function for inserting a element in a given index
void Array::Insert(int index, int x){
    if(index>=0 && index<=length){
        for(int i=length; i>index; i--)
            A[i]=A[i-1];
        A[index]=x;
        length++;
    }
}

//function for deleting a given index element

int Array::Delete(int index){
    int x=0;
    if(index>0 && index<=length){
        x=A[index];
        for(int i=index; i<length-1; i++){
            A[i]=A[i+1];
        }
        length--;
        return x;
    }
    return 0;
}

//function to swap two numbers or elements
void Array::swap(int *x, int *y){
    int temp;
    temp=*x;
    *x=*y;
    *y=temp;
}

//function to find the index of the given element by linear search
int Array::LinearSearch(int key){
    for(int i=0; i<length; i++){
        if(key==A[i]){
            return i;
        }
    }
    return -1;
}
//function to find the index of the given element by Binary search

int Array::BinarySearch(int key){
    int l=0,h=length-1, mid;
    while(l<=h){
        mid=(l+h)/2;
        if(key==A[mid])
            return mid;
        else if(key>A[mid])
            l=mid+1;
        else
            h=mid-1;
    }
    return -1;
}

//Function to find an element

int Array::Get(int index){
    if(index>=0 && index<length){
        return A[index];
    }
    return -1;
}

//Function to set a element at given index
void Array::set(int index, int x){
    if(index>=0 && index<length){
        A[index]=x;
    }
}

//Function to find the maximum element of an array
int Array::Max(){
    int max=A[0];
    for(int i=0; i<length; i++){
        if(max<A[i])
            max=A[i];
    }
    return max;
}

//Functin to find the minimum element of an array
int Array::Min(){
    int min=A[0];
    for(int i=0; i<length; i++){
        if(min>A[i])
            min=A[i];
    }
    return min;
}

//Function to find the sum of an array
int Array::sum(){
    int x=0;
    for(int i=0; i<length; i++){
        x+=A[i];
    }
    return x;
}

//Function to find the average of the elements of the array
float Array::Avg(){
    return (float)sum()/length;
}

//Function to reverse the array
void Array::Reverse(){
    int *B;
    B=new int[length];
    for(int i=length-1,j=0; i>=0; i--,j++){
        B[j]=A[i];
    }
    for(int i=0; i<length; i++){
        A[i]=B[i];
    }
}

//Function to reverse the array without auixilary array
void Array::Reverse2(){
    for(int i=0, j=length-1; i<j; i++,j--){
        swap(&A[i],&A[j]);
    }
}

//Function to insert an element in sorted array

void Array::InsertSort(int x){
    int i=length-1;
    if(length==size)
        return;
    while(i>=0 && A[i]>x){
        A[i+1]=A[i];
        i--;
    }
    A[i+1]=x;
    length++;
}

//Function to check whether the array is sorted or not
int Array::isSorted(){
    for(int i=0; i<length-1; i++){
        if(A[i]>A[i+1])
            return 0;
    }
    return 1;
}

//Function to arrange the negative and positive numbers in an array
void Array::Rearrange(){
    int i=0, j=length-1;
    while(i<j){
        while(A[i]<0){i++;}
        while(A[j]>0){j--;}
        if(i<j)
            swap(&A[i], &A[j]);
    }
}

//Function to merging two sorted arrays
Array *Array::Merge(Array arr2){
    int i=0,j=0,k=0;
    Array *arr3=new Array(length+arr2.length);
    while(i<length && j<arr2.length){
        if(A[i]<arr2.A[j]){
            arr3->A[k++]=A[i++];
        }else{
            arr3->A[k++]=arr2.A[j++];
        }
    }
    for(; i<length; i++){
        arr3->A[k++]=A[i++];
    }
    for(; j<arr2.length; j++){
        arr3->A[k++]=arr2.A[j++];
    }
    arr3->length=length+arr2.length;
    return arr3;
}

//Function to find union of two sorted arrays

Array *Array::Union(Array arr2){
    int i=0,j=0,k=0;
    Array *arr3=new Array(length+arr2.length);
    while(i<length && j<arr2.length){
        if(A[i]<arr2.A[j]){
            arr3->A[k++]=A[i++];
        }else if(A[i]>arr2.A[j]){
            arr3->A[k++]=arr2.A[j++];
        }else{
            arr3->A[k++]=A[i++];
            j++;
        }
    }
    for(; i<length; i++){
        arr3->A[k++]=A[i++];
    }
    for(; j<arr2.length; j++){
        arr3->A[k++]=arr2.A[j++];
    }
    arr3->length=k;
    return arr3;
}

//Function to find intersection of two arrays
Array *Array::Intersection(Array arr2){
    int i=0,j=0,k=0;
   Array *arr3=new Array(length+arr2.length);
    while(i<length && j<arr2.length){
        if(A[i]<arr2.A[j]){
            i++;
        }else if(A[i]>arr2.A[j]){
            j++;
        }else{
            arr3->A[k++]=A[i++];
            j++;
        }
    }
    for(; i<length; i++){
        arr3->A[k++]=A[i++];
    }
    for(; j<arr2.length; j++){
        arr3->A[k++]=arr2.A[j++];
    }
    arr3->length=k;
    return arr3;
}

//Function to find the difference of two sorted arrays

Array *Array::Difference(Array arr2){
    int i=0,j=0,k=0;
    Array *arr3=new Array(length+arr2.length);
    while(i<length && j<arr2.length){
        if(A[i]<arr2.A[j]){
            arr3->A[k++]=A[i++];
        }else if(A[i]>arr2.A[j]){
            j++;
        }else{
            i++;
            j++;
        }
    }
    for(; i<length; i++){
        arr3->A[k++]=A[i++];
    }
    arr3->length=k;
    return arr3;
}
//Main funciton

int main()
{
    Array *arr1;
    int ch, sz;
    int x, index;
    
    cout<<"Enter the size of the array: ";
    cin>>sz;
    arr1=new Array[sz];
    
    do{
        cout<<"\n\nMenu\n";
        cout<<"1. Insert\n";
        cout<<"2. Delete\n";
        cout<<"3. Search\n";
        cout<<"4, Sum\n";
        cout<<"5. Max of an array\n";
        cout<<"6. Min of an array\n";
        cout<<"7.Average of an array\n ";
        cout<<"8. Display the elements of an array\n ";
        cout<<"9. Exit\n";
        
        cout<<"Enter the choice: ";
        cin>>ch;
        
        switch(ch){
            case 1: cout<<"Enter an element and index ";
                    cin>>x>>index;
                    arr1->Insert(index,x);
                    break;
            case 2: cout<<"Enter an index: ";
                    cin>>index;
                    x=arr1->Delete(index);
                    cout<<"Deleted element is "<<x;
                    break;
            case 3: int choice;
                    cout<<"1. Linear search\n";
                    cout<<"2. Binary Search\n ";
                    cout<<"Choose method to search";
                    cin>>choice;
                    switch(choice){
                        case 1: cout<<"Enter the element which you want to search ";
                                cin>>x;
                                index=arr1->LinearSearch(x);
                                cout<<"Element index is: "<<index;
                                break;
                        case 2: cout<<"Enter the element which you want to search ";
                                cin>>x;
                                index=arr1->BinarySearch(x);
                                cout<<"Element index is: "<<index;
                                break;        
                    }
                    
            case 4: cout<<"Sum is: "<<arr1->sum();
                    break;
            case 5: cout<<"Maximum Element of array is: "<<arr1->Max();
                    break;
            case 6: cout<<"Minimum Element of array is: "<<arr1->Min();
                    break;
            case 7: cout<<"Average of array is: "<<arr1->Avg();
                    break;        
            case 8: arr1->Display();
            
        }
    }while(ch<9);

    return 0;
}
