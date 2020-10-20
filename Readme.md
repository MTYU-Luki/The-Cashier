# The Cashier
Aplikasi yang berfungsi untuk meghitung harga Barang/Jasa, seperti pada kasir yang ada di supermarket hanya saja aplikasi ini belum kompleks dan belum ada database dan harus menginput secara manual

# Scope & Functionalities
- user dapat menginputkan nama item
- user dapat memilih bagian type mau jasa/barang
- user dapat menginputkan jumlah item yang akan di tambahkan
- user dapat menginputkan harga dalam satuan rupiah

# How Does it Works?
Diawali pendeklarasian method sebagai awalan untuk menjalankan method `MainWindows()` pada class `MainWindows.Xaml.cs` atau perintah yang ada di dalamnya.

```csharp
public MainWindow()
        {
            InitializeComponent();
            calculator = new Calculator(); //membuat objek calculator dari class Calculator
            listBox.ItemsSource = calculator.getListItem(); //memasukan listitem ke list box yang di dapat dari getListItem();
        }
```

Kemudian pada method `AddButton_Click()`, method ini menerima value dari inputan user dari `MainWindow.xaml` kemudian di proses pada class `item`, setelah itu kemudian
dimasukan lagi di class `Calculator` baru sampai ke method `AddButton_Click()`.

```csharp
private void AddButton_Click(object sender, RoutedEventArgs e)
        {
            string title = itemNameBox.Text; //mengambil dari class item
            int quantity = int.Parse(quantityBox.Text); //int.parsh berguna untuk mengubah string ke int
            string type = typeBox.Text;
            double price = double.Parse(priceBox.Text);// double.parsh berguna untuk mengubah string ke double

            Item item = new Item(new Random().Next(), title, quantity, price, price, type);
            calculator.addItem(item); //menambahkan fungsi additem yang da pada class calculator
            double total = calculator.getTotal();

            totalLabel.Content = string.Format("Rp. {0}", total);

            listBox.Items.Refresh();// akan merefres ketika button ADD ditekan

        }
```
 Prinsip pengunaan Single Reponsibility terdapat pada class `Calculator`. Class ini menambahkan 
item yang diinputkan oleh user dari `MainWindow.xaml` kedalam sebuah list dan dihitung totalnya.

```csharp
public void addItem(Item item)
        {
            this.listItem.Add(item);
            this.total += item.getSubTotal();
        }
```

kemudian jika pada quintity diinputkan berupa huruf akan terjadi force close pada mainwindownya

>jika ada kesalah kata , atau penjelasan mohon dimaafkan sekian dan terimakasih