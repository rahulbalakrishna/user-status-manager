<?php
	$url = get_base_url();
	$file_url = $url."/wp-config.php";
	require($file_url);
	
	global $wpdb;
	$table = $wpdb->prefix . 'user_status_manager';
	$table_user = $wpdb->prefix . 'users';
	
	$user_id   = $_POST['user_id'];
	$from_date = $_POST['from_date'];
	$to_date   = $_POST['to_date'];
	
	if(isset($_POST['user_id']) && !empty($_POST['user_id'])){
		$user_id_arr = explode(",",$_POST['user_id']);
	}
	
	$from_date_arr = explode(",",$_POST['from_date']);
	$to_date_arr   = explode(",",$_POST['to_date']);
	$status   = explode(",",$_POST['status']);
	
	$user_id_count = count($user_id_arr);
	
	for($i=0;$i<$user_id_count;$i++){
		$result = $wpdb->get_row('select id from '.$table.' where user_id = '.$user_id_arr[$i]);
		$value = $wpdb->get_row('select ID,user_login,user_email from '.$table_user.' where ID='.$user_id_arr[$i]);
		if(count($result)>0){
			//update
			
			$update_val = array(
									'user_id' 	  => $value->ID,
									'user_name'   => $value->user_login,
									'user_email'  => $value->user_email,
									'status_from' => $from_date_arr[$i],
									'status_to'   => $to_date_arr[$i],
									'status'	  => $status[$i]
								);
			$where = array(
								'user_id' 	  => $value->ID
							);
			if($wpdb->update($table,$update_val,$where)){
				echo "yes";
			}else{
				echo "no";
			}
		}else{
			//insert
			$update_val = array(
									'user_id' 	  => $value->ID,
									'user_name'   => $value->user_login,
									'user_email'  => $value->user_email,
									'status_from' => $from_date_arr[$i],
									'status_to'   => $to_date_arr[$i],
									'status'	  => $status[$i]
								);
			if($wpdb->insert( $table, $update_val)){
				echo "yes";
			}else{
				echo "no";
			}
		}
	}
		
	
	function get_base_url(){
	$root_dir = $_SERVER['DOCUMENT_ROOT'];
	
        /* returns /myproject/index.php */
        $path = $_SERVER['PHP_SELF'];

        /*
         * returns an array with:
         * Array (
         *  [dirname] => /myproject/
         *  [basename] => index.php
         *  [extension] => php
         *  [filename] => index
         * )
         */
        $path_parts = pathinfo($path);
        $directory = $path_parts['dirname'];
        /*
         * If we are visiting a page off the base URL, the dirname would just be a "/",
         * If it is, we would want to remove this
         */
		$dir =explode('/',$directory);
        $directory = ($directory == "/") ? "" : $dir;

        /* Returns localhost OR mysite.com */
        //$host = $_SERVER['HTTP_HOST'];
		$directory[1] = str_replace("wp-content", "", $directory[1]);
        return  $root_dir ."/".$directory[1];
	}
?>