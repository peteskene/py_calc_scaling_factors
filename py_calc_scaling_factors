from subprocess import check_output
import pandas as pd

def py_calc_scaling_factors(list_files, file_type, multiplying_factor=10000.0):
    
    """
    written by peteskene@gmail.com
    
    script takes in a list of files (can include path)
    file_type = 'bed' OR 'sam' (provide as a string)
    e.g. list_files = ['A.bed', 'B.bed', 'C.bed'] OR ['A.sam', 'B.sam', 'C.sam']
         
    Script counts the number of sequenced fragments (for sam files, expects paired end reads,
    so number of fragments is half the number of reads; for bed files, counts number of lines)
    
    scaling factor = multiplying_factor / number of sequenced fragments
    
    returns a list of scaling factors (order is same as list_files)
        
    """
    
    print 'Files imported: '
    print '\n'.join(list_files)
    print
    
    if file_type not in ['sam', 'bed']:
        return "Exiting... file_type needs to be set as either 'bed' or 'sam'"
    
    print 'file_type set to: ' + file_type
    print
    
    sequence_count = []
    
    for item in list_files:
        print 'operating on: ' + item
        
        if file_type=='sam':
            temp_str = 'samtools view -c -S ' + item
            temp_value = int(check_output(temp_str, shell =True))/2
            sequence_count.append(temp_value)
            print 'sequence count: ' + str(temp_value)
            
        if file_type=='bed':
            temp_df = pd.read_csv(item, sep='\t', header=None)
            temp_value = len(temp_df.index)
            sequence_count.append(temp_value)
            print 'sequence count: ' + str(temp_value)
        print
            
    scaling_factors = [multiplying_factor/float(item) for item in sequence_count]
    
    print 'scaling factors to be returned as list: '
    print '\n'.join([str(item) for item in scaling_factors])
    print           
    
    return scaling_factors
