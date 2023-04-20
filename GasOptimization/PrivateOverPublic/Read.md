#### Custom function to get all the constants(private) 
 function getConstants()
        external
        pure
        returns (
            uint256 _LTV_PRECISION,
            uint256 _LIQ_PRECISION,
            uint256 _UTIL_PREC,
            uint256 _FEE_PRECISION,
            uint256 _EXCHANGE_PRECISION,
            uint64 _DEFAULT_INT,
            uint16 _DEFAULT_PROTOCOL_FEE,
            uint256 _MAX_PROTOCOL_FEE
        )
    {
        _LTV_PRECISION = LTV_PRECISION;
        _LIQ_PRECISION = LIQ_PRECISION;
        _UTIL_PREC = UTIL_PREC;
        _FEE_PRECISION = FEE_PRECISION;
        _EXCHANGE_PRECISION = EXCHANGE_PRECISION;
        _DEFAULT_INT = DEFAULT_INT;
        _DEFAULT_PROTOCOL_FEE = DEFAULT_PROTOCOL_FEE;
        _MAX_PROTOCOL_FEE = MAX_PROTOCOL_FEE;
    }
