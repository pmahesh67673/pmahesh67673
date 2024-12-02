
#include <stdio.h>
#include <math.h>

int main() {
    // Hard-coded variables
    double a = 0.002;   // Coefficient for quadratic term
    double b = 0.5;     // Coefficient for linear term
    double c = 20;      // Constant term (base temperature)
    double x;           // Time or other independent variable
    double temperature; // Resulting temperature

    // Asking for input
    printf("Enter the value of x (time or other variable): ");
    scanf("%lf", &x);

    // Quadratic equation for temperature
    temperature = a * pow(x, 2) + b * x + c;

    // Output the result
    printf("The predicted temperature at x = %.2lf is %.2lf\n", x, temperature);

    return 0;
}

output:Enter the value of x (time or other variable): 10
The predicted temperature at x = 10.00 is 120.00


#include <stdio.h>
#include <math.h>

int main() {
    // File pointer and input file name
    FILE *file;
    char filename[] = "input.txt";  // File containing x values
    double a = 0.002;   // Coefficient for quadratic term
    double b = 0.5;     // Coefficient for linear term
    double c = 20;      // Constant term (base temperature)
    double x;           // Time or other independent variable
    double temperature; // Resulting temperature

    // Open the file for reading
    file = fopen(filename, "r");
    if (file == NULL) {
        printf("Error opening the file.\n");
        return 1;
    }

    // Read values from the file and calculate temperature
    while (fscanf(file, "%lf", &x) != EOF) {
        // Quadratic equation for temperature
        temperature = a * pow(x, 2) + b * x + c;
        
        // Output the result
        printf("For x = %.2lf, the predicted temperature is %.2lf\n", x, temperature);
    }

    // Close the file
    fclose(file);
    
    return 0;
}

Input File (input.txt):1
5
10
15
20

output:For x = 1.00, the predicted temperature is 20.50
For x = 5.00, the predicted temperature is 40.50
For x = 10.00, the predicted temperature is 120.00
For x = 15.00, the predicted temperature is 225.00
For x = 20.00, the predicted temperature is 360.00

#include <stdio.h>
#include <math.h>

int main() {
    // File pointers and input/output file names
    FILE *inputFile, *outputFile;
    char inputFilename[] = "input.txt";  // File containing x values
    char outputFilename[] = "output.txt"; // File to store the results

    // Coefficients for the quadratic equation
    double a = 0.002;  // Coefficient for quadratic term
    double b = 0.5;    // Coefficient for linear term
    double c = 20;     // Constant term (base temperature)

    // Variables for reading input and calculating temperature
    double x, temperature;

    // Open the input file for reading
    inputFile = fopen(inputFilename, "r");
    if (inputFile == NULL) {
        printf("Error opening the input file.\n");
        return 1;
    }

    // Open the output file for writing
    outputFile = fopen(outputFilename, "w");
    if (outputFile == NULL) {
        printf("Error opening the output file.\n");
        fclose(inputFile);
        return 1;
    }

    // Read the values from the input file and process them
    while (fscanf(inputFile, "%lf", &x) != EOF) {
        // Apply the quadratic formula to calculate temperature
        temperature = a * pow(x, 2) + b * x + c;

        // Write the results to the output file
        fprintf(outputFile, "For x = %.2lf, the predicted temperature is %.2lf\n", x, temperature);
    }

    // Close both the input and output files
    fclose(inputFile);
    fclose(outputFile);

    printf("Results have been saved to %s.\n", outputFilename);
    
    return 0;
}

 Input File (input.txt):1
5
10
15
20

output:For x = 1.00, the predicted temperature is 20.50
For x = 5.00, the predicted temperature is 40.50
For x = 10.00, the predicted temperature is 120.00
For x = 15.00, the predicted temperature is 225.00
For x = 20.00, the predicted temperature is 360.00

#include <stdio.h>
#include <math.h>

int main() {
    // File pointers and input/output file names
    FILE *inputFile, *outputFile;
    char inputFilename[] = "input.txt";  // File containing x values
    char outputFilename[] = "output.txt"; // File to store the results

    // Coefficients for the quadratic equation
    double a = 0.002;  // Coefficient for quadratic term
    double b = 0.5;    // Coefficient for linear term
    double c = 20;     // Constant term (base temperature)

    // Variables for reading input and calculating temperature
    double x, temperature;

    // Open the input file for reading
    inputFile = fopen(inputFilename, "r");
    if (inputFile == NULL) {
        printf("Error: Unable to open the input file '%s'. Please ensure the file exists and is readable.\n", inputFilename);
        return 1;
    }

    // Open the output file for writing
    outputFile = fopen(outputFilename, "w");
    if (outputFile == NULL) {
        printf("Error: Unable to open the output file '%s' for writing.\n", outputFilename);
        fclose(inputFile);
        return 1;
    }

    // Read the values from the input file and process them
    int lineNumber = 1;
    while (fscanf(inputFile, "%lf", &x) != EOF) {
        // Check for valid input (x should be a number)
        if (ferror(inputFile)) {
            printf("Error reading data from file at line %d. Skipping invalid input.\n", lineNumber);
            clearerr(inputFile);
            lineNumber++;
            continue;
        }

        // Apply the quadratic formula to calculate temperature
        temperature = a * pow(x, 2) + b * x + c;

        // Check if the temperature is within a realistic range (example: non-negative temperature)
        if (temperature < -100 || temperature > 1000) {
            printf("Warning: Calculated temperature %.2lf for x = %.2lf is unrealistic. Skipping this value.\n", temperature, x);
        } else {
            // Write the results to the output file
            fprintf(outputFile, "For x = %.2lf, the predicted temperature is %.2lf\n", x, temperature);
        }

        lineNumber++;
    }

    // Close both the input and output files
    fclose(inputFile);
    fclose(outputFile);

    printf("Processing complete. Results have been saved to '%s'.\n", outputFilename);
    
    return 0;
}

input file:1
5
10
15
20
-1000
abc
25
 output:For x = 1.00, the predicted temperature is 20.50
For x = 5.00, the predicted temperature is 40.50
For x = 10.00, the predicted temperature is 120.00
For x = 15.00, the predicted temperature is 225.00
For x = 20.00, the predicted temperature is 360.00
Warning: Calculated temperature 1020000.00 for x = -1000.00 is unrealistic. Skipping this value.
Warning: Skipping invalid input 'abc' at line 6.
For x = 25.00, the predicted temperature is 545.00

#include <stdio.h>
#include <math.h>

int main() {
    // File pointers and input/output file names
    FILE *inputFile, *dataFile;
    char inputFilename[] = "input.txt";  // File containing x values
    char dataFilename[] = "data.txt";    // File to store the x and temperature values

    // Coefficients for the quadratic equation
    double a = 0.002;  // Coefficient for quadratic term
    double b = 0.5;    // Coefficient for linear term
    double c = 20;     // Constant term (base temperature)

    // Variables for reading input and calculating temperature
    double x, temperature;

    // Open the input file for reading
    inputFile = fopen(inputFilename, "r");
    if (inputFile == NULL) {
        printf("Error: Unable to open the input file '%s'. Please ensure the file exists and is readable.\n", inputFilename);
        return 1;
    }

    // Open the data file for writing
    dataFile = fopen(dataFilename, "w");
    if (dataFile == NULL) {
        printf("Error: Unable to open the data file '%s' for writing.\n", dataFilename);
        fclose(inputFile);
        return 1;
    }

    // Read the values from the input file and process them
    while (fscanf(inputFile, "%lf", &x) != EOF) {
        // Apply the quadratic formula to calculate temperature
        temperature = a * pow(x, 2) + b * x + c;

        // Write the x and temperature values to the data file
        fprintf(dataFile, "%.2lf %.2lf\n", x, temperature);
    }

    // Close both the input and data files
    fclose(inputFile);
    fclose(dataFile);

    printf("Data has been saved to '%s'.\n", dataFilename);
    
    return 0;
}

output:1.00 20.50
5.00 40.50
10.00 120.00
15.00 225.00
20.00 360.00
25.00 545.00
