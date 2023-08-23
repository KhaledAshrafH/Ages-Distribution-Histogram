# Ages Distripution Histogram using MPI and OpenMP

This program implements a histogram using the Message Passing Interface (MPI) and OpenMP. The histogram is constructed based on a dataset containing group ages that watch a specific TV show. The program calculates the frequency of age groups and generates a frequency histogram to visually represent the data.

## Requirements

To run this program, you need the following:

- MPI library installed (e.g., Open MPI, MPICH)
- OpenMP library installed (compatible with your compiler)
- C/C++ compiler (supporting MPI and OpenMP)

## Code Input

The program expects the following inputs:

1. Number of bars: Number of intervals or bins the range of values will be divided into.
2. Number of points: Total number of data points in the dataset.
3. Number of Threads: Number of threads to be used for parallel computation with OpenMP.
4. Number of Processes: Number of processes to be used for parallel computation with MPI.

The dataset is assumed to be stored in a file named `dataset.txt`.

## Code Output

The program generates the following output:

- The range of each interval/bar along with the count of data points falling into that interval.

Example output:
```
The range starts with 0 and ends with 6 with a count of 2
The range starts with 6 and ends with 12 with a count of 6
The range starts with 12 and ends with 18 with a count of 4
The range starts with 18 and ends with 24 with a count of 8
```

## Implementation Details

The program utilizes both MPI and OpenMP to achieve parallel computation.

### MPI (Message Passing Interface)

The MPI library is used to distribute the dataset among multiple processes and gather the results.

1. Data Distribution:

   - The dataset is divided equally among the available processes.
   - Each process reads its portion of the dataset from the file.

2. Data Gathering:

   - MPI communication functions, such as `MPI_Scatter` and `MPI_Gather`, are used to distribute and gather data, respectively.
   - The root process (rank 0) receives the data from all processes and merges it into a single dataset.

### OpenMP (Multi-threading)

The OpenMP library is used for parallel computation within each process, utilizing multiple threads.

1. Thread Distribution:

   - The root process distributes the merged dataset evenly among the available threads.
   - Each thread calculates the frequency of age groups in its portion of the dataset.

2. Thread Synchronization:

   - OpenMP synchronization constructs, such as `omp barrier` and `omp critical`, are used to ensure correct accumulation of frequency counts from each thread.

### Histogram Calculation

1. Interval Calculation:

   - The program divides the age range into intervals based on the number of bars specified.
   - The range is determined by dividing the total range of ages by the number of bars.

2. Frequency Counting:

   - Each thread counts the number of data points falling into its assigned interval.
   - The thread-local counts are accumulated to obtain the final frequency counts for each interval.

3. Output Generation:

   - The results are then printed to the console, showing the range of each interval and the count of data points within it.

## How to Run the Code

1. Ensure that you have MPI and OpenMP installed on your system.
2. Compile the code using the appropriate compiler for MPI and OpenMP.
3. Execute the compiled program, providing the required inputs as prompted.
4. The program will read the dataset from the file named "dataset.txt".
5. After processing, the program will display the frequency histogram on the console.

## Dataset Format

The dataset should be stored in a text file named `dataset.txt`. Each line of the file represents a data point, which should be a valid age value. The program assumes that the dataset file is properly formatted and contains one age value per line.

## Error Handling

The program currently assumes that the input values provided are valid. However, for robustness, you may need to add error handling and input validation to handle incorrect inputs. Additionally, file read errors should be handled gracefully.

## Further Improvements

Here are some potential improvements for the program:

- Error handling and input validation can be added to handle incorrect inputs and file read errors.
- The program can be extended to support different data types and formats for the dataset.
- Additional statistical calculations, such as mean and standard deviation, can be included.
- Visualization libraries can be integrated to generate a graphical representation of the histogram.


## Contributing

Contributions are welcome! If you find any issues or have suggestions for improvement, please open an issue or submit a pull request.


## Authors

- [Khaled Ashraf Hanafy Mahmoud - 20190186](https://github.com/KhaledAshrafH).
- [Ahmed Sayed Hassan Youssef - 20190034](https://github.com/AhmedSayed117).
- [Samah Moustafa Hussien Mahmoud - 20190248](https://github.com/Samah-20190248).

## License

This program is licensed under the [MIT License](LICENSE.md).
