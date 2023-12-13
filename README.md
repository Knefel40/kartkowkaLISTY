<Window x:Class="kartkowkalisty.MainWindow"
        xmlns="http://schemas.microsoft.com/winfx/2006/xaml/presentation"
        xmlns:x="http://schemas.microsoft.com/winfx/2006/xaml"
        xmlns:d="http://schemas.microsoft.com/expression/blend/2008"
        xmlns:mc="http://schemas.openxmlformats.org/markup-compatibility/2006"
        xmlns:local="clr-namespace:kartkowkalisty"
        mc:Ignorable="d"
        Title="MainWindow" Height="450" Width="800">
    <Grid>
        <StackPanel>
            <DataGrid ItemsSource="{Binding Samochody}">

            </DataGrid>
            <DataGrid
                        ItemsSource="{Binding Samochody}"
                        CanUserDeleteRows="False"
                        CanUserReorderColumns="False"
                        CanUserSortColumns="False"
                        IsReadOnly="True"
                        AlternatingRowBackground="Pink"
                        AlternationCount="3"
                        RowBackground="White"
                        >


            </DataGrid>
            <Separator/>
            <DataGrid 
                    ItemsSource="{Binding Produkty}"
                        AutoGenerateColumns="False" SelectionChanged="DataGrid_SelectionChanged">
                <DataGrid.Columns>
                    <DataGridComboBoxColumn Header="Marka"
                                                    x:Name="kategoria_data_grid"
                                                    SelectedItemBinding="{Binding Marka}"
                                                    />
                    <DataGridTextColumn Header="Model"
                                                Binding="{Binding Model}"/>
                    <DataGridTextColumn Header="Rocznik"
                                                Binding="{Binding Rocznik}"/>
                    <DataGridTextColumn Header="Kolor"
                                                Binding="{Binding Kolor}"/>
                    <DataGridCheckBoxColumn Header="Dostępność"
                                                    Binding="{Binding Dostepny}"/>

                </DataGrid.Columns>
            </DataGrid>

        </StackPanel>
    </Grid>
</Window>



SKRYPT


using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;
using System.Windows;
using System.Windows.Controls;
using System.Windows.Data;
using System.Windows.Documents;
using System.Windows.Input;
using System.Windows.Media;
using System.Windows.Media.Imaging;
using System.Windows.Navigation;
using System.Windows.Shapes;

namespace kartkowkalisty
{
    /// <summary>
    /// Interaction logic for MainWindow.xaml
    /// </summary>
    public partial class MainWindow : Window
    {
        
        public List<Samochody> Produkty { get; set; }
        public Samochody ZaznaczonyElement { get; set; }
        public MainWindow()
        {
            InitializeComponent();
            DataContext = this;
            przygotujDane();

        }
        private void przygotujDane()
        {
            Produkty = new List<Samochody>();
            Produkty.Add(new Samochody("Audi", "A3", "2005 ", "niebieski", true));
            Produkty.Add(new Samochody("Opel", "Astra", "2000 ", "niebieski", false));
            Produkty.Add(new Samochody("Reno", "Clio", "2006 ", "niebieski", false));
            Produkty.Add(new Samochody("Mercedes", "E63", "2022 ", "niebieski", false));
            kategoria_data_grid.ItemsSource = new List<string>() { "Audi", "Opel", "Mercedes","Reno" };
        }

        private void DataGrid_SelectionChanged(object sender, SelectionChangedEventArgs e)
        {

        }
    }
}



KLASA SAMOCHODY


using System;
using System.Collections.Generic;
using System.Linq;
using System.Text;
using System.Threading.Tasks;

namespace kartkowkalisty
{
    public class Samochody
    {
        public String Marka { get; set; }
        public string Model { get; set; }
        public string Rocznik { get; set; }
        public string Kolor { get; set; }
        public bool Dostepny { get; set; }

        public Samochody(string model, string rocznik, string kolor, bool dostepny)
        {
            Marka = "Audi";
            Model = model;
            Rocznik = rocznik;
            Kolor = kolor;
            Dostepny = dostepny;
        }
        public Samochody(string marka, string model, string rocznik, string kolor, bool dostepny) : this(model, rocznik, kolor, dostepny)
        {
            Marka = marka;
        }
    }
}
