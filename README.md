# Student_Performance_Analysis

clc;
clear;
close all;

marks = [68 74 71;
         81 77 84;
         59 63 61;
         91 88 93;
         73 69 76;
         47 55 52;
         86 90 87;
         64 67 62;
         78 82 80;
         53 58 56;
         95 92 97;
         70 75 73];

attendance = [74 83 66 97 79 52 91 68 86 57 99 76];

totalMarks = sum(marks, 2);
averageMarks = mean(marks, 2);
percentage = totalMarks / 300 * 100;

disp('TOTAL MARKS:');
disp(totalMarks);

disp('AVERAGE MARKS:');
disp(averageMarks);

disp('PERCENTAGE:');
disp(percentage);

passed = sum(averageMarks >= 40);

disp('NUMBER OF STUDENTS PASSED:');
disp(passed);

[topMarks, topStudent] = max(averageMarks);
[lowMarks, lowStudent] = min(averageMarks);

disp(['Topper is Student ', num2str(topStudent)]);
disp(['Topper Marks: ', num2str(topMarks)]);

disp(['Lowest is Student ', num2str(lowStudent)]);
disp(['Lowest Marks: ', num2str(lowMarks)]);

disp('MEAN:');
disp(mean(averageMarks));

disp('MEDIAN:');
disp(median(averageMarks));

disp('MODE:');
disp(mode(averageMarks));

disp('RANGE:');
disp(max(averageMarks)-min(averageMarks));

disp('VARIANCE:');
disp(var(averageMarks));

disp('STANDARD DEVIATION:');
disp(std(averageMarks));

figure;
histogram(averageMarks, 5);
xlabel('Average Marks');
ylabel('Number of Students');
title('Distribution of Average Marks');
grid on;

c = corrcoef(attendance, averageMarks');

disp('CORRELATION:');
disp(c(1,2));

disp('R-SQUARED:');
disp(c(1,2)^2);

p = polyfit(attendance, averageMarks', 1);
predicted = polyval(p, attendance);

disp('SLOPE AND INTERCEPT:');
disp(p);

prediction = polyval(p, 80);

disp('PREDICTED MARKS AT 80% ATTENDANCE:');
disp(prediction);

figure;
plot(attendance, averageMarks', 'bo');
hold on;
plot(attendance, predicted, 'm', 'LineWidth', 2);
xlabel('Attendance (%)');
ylabel('Average Marks');
title('Attendance vs Marks');
legend('Actual Marks', 'Regression Line');
grid on;
hold off;

groupA = averageMarks(1:6);
groupB = averageMarks(7:12);

[h, pValue] = ttest2(groupA, groupB);

disp('T-TEST RESULT:');
disp(h);

disp('P-VALUE:');
disp(pValue);

if h == 1
    disp('Significant difference between two groups.');
else
    disp('No significant difference between two groups.');
end

disp('========== PROJECT SUMMARY ==========');

disp(['Total Students: ', num2str(length(averageMarks))]);
disp(['Class Average: ', num2str(mean(averageMarks))]);
disp(['Average Attendance: ', num2str(mean(attendance))]);

