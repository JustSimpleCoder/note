

windows 10 sublime 3 安装phpcs
-
1. package install  phpcs
2. 下载 [PHP_CodeSniffer](http://pear.php.net/package/PHP_CodeSniffer/download)  **解压文件（任意，建议解压php环境目录中 例如 e:\php\PHP_CodeSniffer）后期需修改此文件**
3. 下载 [php-cs-fixer-v2.phar](http://cs.sensiolabs.org)
4. 修改配置文件 php code sniffer-> setting user 配置如下

	`


	    // Example for:
	    // - Windows 7
	    // - With phpcs and php-cs-fixer support

	    // We want debugging on
	    "show_debug": true,

	    // Only execute the plugin for php files
	    "extensions_to_execute": ["php"],

	    // Do not execute for twig files
	    "extensions_to_blacklist": ["twig.php"],

	    // Execute the sniffer on file save
	    "phpcs_execute_on_save": true,

	    // Show the error list after save.
	    "phpcs_show_errors_on_save": true,

	    // Show the errors in the gutter
	    "phpcs_show_gutter_marks": true,

	    // Show outline for errors
	    "phpcs_outline_for_errors": true,

	    // Show the errors in the status bar
	    "phpcs_show_errors_in_status": true,

	    // Show the errors in the quick panel so you can then goto line
	    "phpcs_show_quick_panel": true,

	    // Path to php on windows installation
	    // This is needed as we cannot run phars on windows, so we run it through php
	    "phpcs_php_prefix_path": "E:\\software\\phpStudy\\PHPTutorial\\php\\php-7.0.12-nts\\php.exe",

	    // We want the fixer to be run through the php application
	    "phpcs_commands_to_php_prefix": ["Fixer"],


	    // PHP_CodeSniffer settings
	    // Yes, run the phpcs command
	    "phpcs_sniffer_run": true,

	    // And execute it on save
	    "phpcs_command_on_save": true,

	    // This is the path to the bat file when we installed PHP_CodeSniffer
	    "phpcs_executable_path": "E:\\software\\phpStudy\\PHPTutorial\\php\\php-7.0.12-nts\\PHP_CodeSniffer\\scripts\\phpcs.bat",

	    // I want to run the PSR2 standard, and ignore warnings
	    "phpcs_additional_args": {
	        "--standard": "PSR2",
	        "-n": ""
	    },


	    // PHP-CS-Fixer settings
	    // Don't want to auto fix issue with php-cs-fixer
	    "php_cs_fixer_on_save": false,

	    // Show the quick panel
	    "php_cs_fixer_show_quick_panel": true,

	    // The fixer phar file is stored here:
	    "php_cs_fixer_executable_path": "E:\\software\\phpStudy\\PHPTutorial\\php\\php-7.0.12-nts\\php-cs-fixer-v2.phar",

	    // Additional arguments, run all levels of fixing
	    "php_cs_fixer_additional_args": {
	    },


	    // PHP Linter settings
	    // Yes, lets lint the files
	    "phpcs_linter_run": true,

	    // And execute that on each file when saved (php only as per extensions_to_execute)
	    "phpcs_linter_command_on_save": true,

	    // Path to php
	    "phpcs_php_path": "E:\\software\\phpStudy\\PHPTutorial\\php\\php-7.0.12-nts\\php.exe",

	    // This is the regex format of the errors
	    "phpcs_linter_regex": "(?P<message>.*) on line (?P<line>\\d+)",


	    // PHP Mess Detector settings
	    // Not turning on the mess detector here
	    "phpmd_run": false,
	    "phpmd_command_on_save": false,
	    "phpmd_executable_path": "",
	    "phpmd_additional_args": {
	        "codesize,naming,unusedcode": ""
	    }

	`

5. 修改 PHP_CodeSniffer\scripts\phpcs.bat （**修改 php_bin php_dir bin_dir 路径**)  文件如下


`

	@echo off
	REM PHP_CodeSniffer tokenises PHP code and detects violations of a
	REM defined set of coding standards.
	REM
	REM PHP version 5
	REM
	REM @category  PHP
	REM @package   PHP_CodeSniffer
	REM @author    Greg Sherwood <gsherwood@squiz.net>
	REM @author    Marc McIntyre <mmcintyre@squiz.net>
	REM @copyright 2006-2012 Squiz Pty Ltd (ABN 77 084 670 600)
	REM @license   https://github.com/squizlabs/PHP_CodeSniffer/blob/master/licence.txt BSD Licence
	REM @version   CVS: $Id: phpcs.bat,v 1.3 2007-11-04 22:02:16 squiz Exp $
	REM @link      http://pear.php.net/package/PHP_CodeSniffer

	REM "@php_bin@" -d auto_append_file="" -d auto_prepend_file="" -d include_path="'@php_dir@'" -f "@bin_dir@\phpcs" -- %*
	"E:\software\phpStudy\PHPTutorial\php\php-7.0.12-nts\php.exe" -d auto_append_file="" -d auto_prepend_file="" -d include_path="'E:\software\phpStudy\PHPTutorial\php\php-7.0.12-nts\'" -f "E:\software\phpStudy\PHPTutorial\php\php-7.0.12-nts\PHP_CodeSniffer\scripts\phpcs" -- %*

`

