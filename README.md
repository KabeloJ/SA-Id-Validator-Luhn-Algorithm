# How to validate RSA Id number using C# and <a href="https://en.wikipedia.org/wiki/Luhn_algorithm">Luhn's algorithm</a>.

* To RSA Id number is validated using the luhn's algorithm.  See C# Function below:

        using System;
        using System.Collections.Generic;
        using System.Linq;

        namespace Luhn_Algorithm
        {
            class Program
            {
                static void Main(string[] args)
                {
                    Console.WriteLine("Enter SA Id Number: ");
                    string IdNumber = Console.ReadLine();
                    Console.WriteLine(ValidId(IdNumber).ToString());
                    Console.ReadKey();
                }
                static bool ValidId(string idNumber)
                {
                    //IdNumber must not be empty and must be 13 characters
                    if (!string.IsNullOrEmpty(idNumber) && idNumber.Length == 13)
                    {
                        try
                        {

                            int count = 0;
                            List<int> EvensArr = new List<int>();
                            List<int> OddsArr = new List<int>();
                            foreach (var item in idNumber)
                            {
                                count++;
                                if ((count % 2) == 0) // Taking values at Even Index
                                {
                                    string Product = (Convert.ToInt32(item.ToString()) * 2).ToString();
                                    if (Product.Length == 2)
                                    {
                                        Product = Product.Substring(1, 1);
                                        Product = (Convert.ToInt32(Product) + 1).ToString();
                                    }
                                    EvensArr.Add(Convert.ToInt32(Product));
                                }
                                else
                                {
                                    //Storing numbers at odd index
                                    OddsArr.Add(Convert.ToInt32(item.ToString()));
                                }
                            }
                            int SumOfArrays = EvensArr.Sum() + OddsArr.Sum();
                            if ((SumOfArrays % 10) == 0) //Checking if the number is divisible by 10
                            {
                                return true;
                            }
                        }
                        catch (Exception e)
                        {
                            throw e;
                        }
                    }
                    return false;
                }
            }
        }
        
      
The Code above will simply return true if the Id is valid and return false if the Id is invalid.
