```
echo "Error! Enter kWh consumed: \n";
	$kwh = trim(fgets(STDIN));
	}
	return $kwh;
}
function find_amount($kwh) {
	if ($kwh <= 450) {
		$amount = $kwh * 0.07;
	}
	elseif ($kwh <= 2200) {
		$amount = 450 * 0.07 + ($kwh - 450) * 0.20;
	}
	else {
		$amount = 450 * 0.07 + 1750 * 0.20 + ($kwh - 1750) * 0.33;
	}
	$amount += 0.22 * $amount;
	return $amount;
}
do {
	$kwh = get_consumption();
	echo find_amount($kwh);
	echo "Repeat?\n";
	$answer = trim(fgets(STDIN));
	} while (strtoupper($answer) == "YES");
?>
```