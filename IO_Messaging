#!/usr/bin/perl -w

use strict;
use warnings;

use LWP::UserAgent;
use JSON;

use String::Util;

#################################################################################
# Variabili
#################################################################################

my $number_args = $#ARGV + 1;
if ($number_args != 4) {
    print " Inserire: <cf> <importo> <numero_avviso> <servizio>. \n";
    exit;
}
my $cf=$ARGV[0];
my $importo=$ARGV[1];
my $numero_avviso=$ARGV[2];
$numero_avviso = "3" . $numero_avviso;
my $servizio=$ARGV[3];

my $urlmain = "https://api.cd.italia.it/api/v1/messages/";
my $ocpapimsubscriptionkeymain_cie = 'xxx';
my $ocpapimsubscriptionkeymain_tari = 'xxx';
my $ocpapimsubscriptionkeymain_mensa = 'xxx';
my $ocpapimsubscriptionkeymain_benvenuto = 'xxx';
my $ocpapimsubscriptionkeymain_minigrest = 'xxx';

my $subject_cie = "Pagamento CIE";
my $subject_mensa = "Pagamento mensa scolastica";
my $subject_tari = "Pagamento TARI 2019 rata unica";
my $subject_benvenuto = "Benvenuto su IO";
my $subject_minigrest = "Pagamento minigrest";

#################################################################################

&print_now("Inizio del codice: ");

my $message;
my $counter = 0;

my $urlmainparam = $urlmain . $cf; 

my $year; my $mon; my $mday; my $hour; my $min; my $sec; my $wday; my $yday; my $isdst;my $messagecode;
($sec,$min,$hour,$mday,$mon,$year,$wday,$yday,$isdst) = localtime(time);
$messagecode = sprintf("ATCIT%04d%02d%02d%02d%02d%02d", 1900+$year, $mon, $mday, $hour, $min, $sec);

if ($servizio eq "CIE") {
        $message = "E' ora possibile procedere al pagamento dell'importo necessario per l'emissione della Carta di Identita' Elettronica. \n\n";
        $message = $message . "Intestatario: ** " . $cf . "**\n\n";
        $message = $message . "Importo: ** " . $importo . " euro**\n\n";
        $message = $message . "Puoi pagare direttamente dall'app, oppure scegliere un'altra modalita di pagamento\n";
        $message = $message . "come spiegato nella sezione  [PagoPA]( https://www.comune.ripaltacremasca.cr.it/servizi/pago-pa )\n";
        $message = $message . "del sito del Comune di Ripalta Cremasca.\n\n";
        $message = $message . $messagecode;
        send_message($servizio, $counter, $subject_cie, $cf, $message, $urlmainparam, $ocpapimsubscriptionkeymain_cie, $importo*100, $numero_avviso);
}

if ($servizio eq "MENSA") {
        $message = "E' ora possibile ricaricare il tuo credito per l'utilizzo dei servizi di mensa scolastica.\n\n";
        $message = $message . "Importo ricarica: ** " . $importo . " euro**\n\n";
        $message = $message . "Puoi pagare direttamente dall'app, oppure scegliere un'altra modalita di pagamento\n";
        $message = $message . "come spiegato nella sezione  [PagoPA]( https://www.comune.ripaltacremasca.cr.it/servizi/pago-pa )\n";
        $message = $message . "del sito del Comune di Ripalta Cremasca.\n\n";
        $message = $message . $messagecode;
        send_message($servizio, $counter, $subject_mensa, $cf, $message, $urlmainparam, $ocpapimsubscriptionkeymain_mensa, $importo*100, $numero_avviso);
}

if  ($servizio eq "TARI") {
        $message = "Se vuoi procedere al pagamento della TARI (tassa sui rifiuti), da oggi puoi, in un'unica rata!\n\n";
        $message = $message . "Pagamento in una rata unica\n";
        $message = $message . "Scadenza: ** 30 Luglio 2019 ** \n";
        $message = $message . "Importo: ** " . $importo . " euro**\n\n";
        $message = $message . "Puoi pagare direttamente dall'app, oppure scegliere un'altra modalita di pagamento\n";
        $message = $message . "come spiegato nella sezione  [PagoPA]( https://www.comune.ripaltacremasca.cr.it/servizi/pago-pa )\n";
        $message = $message . "del sito del Comune di Ripalta Cremasca.\n\n";
        $message = $message . $messagecode;
        send_message($servizio, $counter, $subject_tari, $cf, $message, $urlmainparam, $ocpapimsubscriptionkeymain_tari, $importo*100, $numero_avviso);
}

if  ($servizio eq "MINIGREST") {
        $message = "E' ora possibile ricaricare il tuo credito per l'utilizzo del servizio minigrest.\n\n";
        $message = $message . "Importo: ** " . $importo . " euro**\n\n";
        $message = $message . "Puoi pagare direttamente dall'app, oppure scegliere un'altra modalita di pagamento\n";
        $message = $message . "come spiegato nella sezione  [PagoPA]( https://www.comune.ripaltacremasca.cr.it/servizi/pago-pa )\n";
        $message = $message . "del sito del Comune di Ripalta Cremasca.\n\n";
        $message = $message . $messagecode;
        send_message($servizio, $counter, $subject_minigrest, $cf, $message, $urlmainparam, $ocpapimsubscriptionkeymain_minigrest, $importo*100, $numero_avviso);
}

if  ($servizio eq "BENVENUTO") {

        $message = "Alcuni servizi del **Comune di Ripalta Cremasca** sono adesso disponibili su IO!\n\n";
        $message = $message . "In particolare potrai:\n\n";
        $message = $message . "- pagare l'importo necessario per l'emissione della CIE (carta di identita' elettronica)\n";
        $message = $message . "- ricaricare il credito per l'utilizzo della mensa scolastica\n";
        $message = $message . "- pagare la Tassa Rifiuti (Tari)\n\n";
        $message = $message . "Per altre informazioni o per contattare il comune di Ripalta Cremasca puoi accedere al sito ";
	$message = $message . "[www.comune.ripaltacremasca.cr.it](www.comune.ripaltacremasca.cr.it). \n\n";
        $message = $message . $messagecode;
        send_message($servizio, $counter, $subject_benvenuto, $cf, $message, $urlmainparam, $ocpapimsubscriptionkeymain_benvenuto, -1, -1);
}

	
&print_now("Fine del codice: ");

sub send_message {
    
	my ($type, $counter, $subject, $cfpiva, $message, $url, $ocpapimsubscriptionkey, $amount, $notice_number) = @_; 
	$amount = $amount + 0;

	my @headers = (                                                      
		'Timeout','30',                                                    
		'Content-Type','application/json',
		'Ocp-Apim-Subscription-Key'
	);                                                                   
	push (@headers, $ocpapimsubscriptionkey);
	
	my $payment_data =  {
		amount => $amount,
		notice_number => $notice_number
  	};

	#print "Messaggio da inviare: $message \n\n";

	##########################################
	# Send Message 
	##########################################

	
	my $ua = LWP::UserAgent->new;
	my %req;
	if ($amount >0) {
		%req = (
			content => {
				subject => $subject,
				markdown => $message,
	        		payment_data => $payment_data
      			}
		)
	} else {
		%req = (
			content => {
				subject => $subject,
				markdown => $message
      			}
		)
	}


	my $post_data = encode_json(\%req);

	my $response = $ua->post($url,
	    content => $post_data,
	    @headers, 
	    'charset' => 'utf-8'
	);

	die "Request failed: ", $response->content unless $response->is_success();

	print " " . $counter . " - " . $type . " - " . $cfpiva . " - " . $response->content, $/;

	$counter++;

}

sub print_now {
	my $year; my $mon; my $mday; my $hour; my $min; my $sec; my $wday; my $yday; my $isdst;my $now;
	($sec,$min,$hour,$mday,$mon,$year,$wday,$yday,$isdst) = localtime(time);
	$now = sprintf("%04d-%02d-%02d %02d:%02d:%02d", 1900+$year, $mon, $mday, $hour, $min, $sec);
	print "\n " . shift . " " . $now . " \n\n";
}



