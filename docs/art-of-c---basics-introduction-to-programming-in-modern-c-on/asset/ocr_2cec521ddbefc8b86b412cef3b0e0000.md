```
crypto.ComputeHash(Encoding.ASCII.GetBytes(initialCode)).ToHex();
			State = LockState.Locked;
		}

		public void Dispose() => crypto.Dispose();

		public bool Lock() {
			if (State == LockState.Locked) {
				return false;
			}
			State = LockState.Locked;
			return true;
		}

		public bool Unlock(string code) {
			if (State == LockState.Unlocked) {
				return false;
			}
			if (crypto.ComputeHash(Encoding.ASCII.GetBytes(code)).ToHex() ==
hash) {
				State = LockState.Unlocked;
				return true;
			}
			return false;
		}

		public bool SetCode(string newCode, string currentCode) {
			if
(currentCode.ComputeHash(Encoding.ASCII.GetBytes(currentCode)).ToHex() ==
hash) {
				if (!IsCodeInValidFormat(newCode)) {
					return false;
				}
				hash =
crypto.ComputeHash(Encoding.ASCII.GetBytes(newCode)).ToHex();
				State = LockState.Locked;
				return true;
			}
			return false;
```