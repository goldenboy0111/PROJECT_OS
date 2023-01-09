#include <stdio.h>
#include <stdlib.h>
#include <getopt.h>
#include <stdbool.h>
#include <string.h>
#include <limits.h>
#define BUFF_SIZE 999999



enum CPUMethods
{
	NONE,
	FCFS,
	SJF,
	PS,
	RR
} method = NONE;
enum PMode
{
	OFF,
	ON
} mode = OFF; 


int time_quantum;
char *input_filename = NULL;
char *output_filename = NULL;
char buff[BUFF_SIZE];
char buffer_output[BUFF_SIZE * 6];
bool fcfs_first = true;
bool sjf_np_first = true;
bool sjf_p_first = true;
bool ps_np_first = true;
bool ps_p_first = true;
bool rr_first = true;
char *exe;


struct node
{
	int process_id;
	int burst_time;
	int arrival_time;
	int priority;
	int waiting_time;
	int turnaround_time;
	int first_response;
	int how_much_left;
	int time_slices;
	int last_slice_burst;
	bool is_terminated;
	bool in_cpu;
	struct node *next;
};
struct node *header_original = NULL;
struct node *create_node(int, int, int, int);
struct node *insert_back(struct node *, int, int, int, int);
struct node *delete_front(struct node *);
void display_LL(struct node *);
struct node *clone_LL();


void print_usage();
void menu();
void menu1();
void menu2();
void menu3();
void menu4();
void tq_menu();
void write_input_to_LL(char *);
void fcfs();
void sjf_np();
void sjf_p();
void ps_np();
void ps_p();						
void rr();					
int process_counter(struct node *);				
struct node *swap_nodes(struct node *, struct node *); 
void bubble_sort(struct node **, int, char *);	
bool is_all_done(struct node *);			
bool is_previous_ones_done(struct node *, int);	
struct node *find_least_left(struct node *, int);
struct node *find_least_priority(struct node *, int); 

int main(int argc, char *argv[])
{
	exe = argv[0];
	int options = 0;

	while ((options = getopt(argc, argv, "f:o:")) != -1)
	{
		switch (options)
		{
		case 'f':
			input_filename = optarg;
			break;
		case 'o':
			output_filename = optarg;
			break;
		default:
			print_usage();
			break;
		}
	}

	if (input_filename == NULL || output_filename == NULL)
	{
		print_usage();
	}

	FILE *finput = fopen(input_filename, "r");
	if (finput == NULL) 
		printf("The argument that you passed as input file does not exists.\n");
		printf("Please check the input file argument and run the program again\n");
		exit(1);
	}
	fclose(finput);

	write_input_to_LL(input_filename);

	menu();

	return 0;
}

